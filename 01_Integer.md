# Integer 的缓存以及自动包装,解包

Integer 是 int 的包装类。

Integer 具有缓存, 范围为: -128 到 +127.

这个机制导致的问题在于:

Java代码:

    public static void testIntegerCache1(){
        System.out.println("------testIntegerCache1-----");
        int num0 = 64;
        Integer num1 = 64;
        Integer num2 = 64;
        Integer num3 = Integer.parseInt("64");
        Integer num4 = Integer.valueOf(64);
        //
        System.out.println(num1 == num2); // true
        System.out.println(num1 == num3); // true
        System.out.println(num1 == num4); // true
        System.out.println("-----");

        // 明确的在堆内存中创建了一个新对象
        Integer num5 = new Integer(64);
        System.out.println(num1 == num5); // false
        System.out.println(num1.equals(num5)); // true
        System.out.println(num0 == num1); // true
    }

    public static void testIntegerCache2(){
        System.out.println("------testIntegerCache2-----");
        int num0 = 128;
        Integer num1 = 128;
        Integer num2 = 128;
        Integer num3 = Integer.parseInt("128");
        Integer num4 = Integer.valueOf(128);
        // 超过了cache范围, 所以每个都是不同的对象
        System.out.println(num1 == num2); // false
        System.out.println(num1 == num3); // false
        System.out.println(num1 == num4); // false
        System.out.println("-----");

        // 明确的在堆内存中创建了一个新对象
        Integer num5 = new Integer(128);
        System.out.println(num1 == num5); // false
        System.out.println(num1.equals(num5)); // true
        System.out.println(num0 == num1); // true
    }


所以对于原生类型, int 可以使用 == 进行比较, 但是对于包装类, 原则上不能使用 == 来进行判定。

这也算是Java的一个坑. 

看看使用 jd-gui 反编译后的代码:


	  public static void testIntegerCache1()
	  {
	    System.out.println("------testIntegerCache1-----");
	    int num0 = 64;
	    Integer num1 = Integer.valueOf(64);
	    Integer num2 = Integer.valueOf(64);
	    Integer num3 = Integer.valueOf(Integer.parseInt("64"));
	    Integer num4 = Integer.valueOf(64);

	    System.out.println(num1 == num2);
	    System.out.println(num1 == num3);
	    System.out.println(num1 == num4);
	    System.out.println("-----");

	    Integer num5 = new Integer(64);
	    System.out.println(num1 == num5);
	    System.out.println(num1.equals(num5));
	    System.out.println(num0 == num1.intValue());
	  }

	  public static void testIntegerCache2() {
	    System.out.println("------testIntegerCache2-----");
	    int num0 = 128;
	    Integer num1 = Integer.valueOf(128);
	    Integer num2 = Integer.valueOf(128);
	    Integer num3 = Integer.valueOf(Integer.parseInt("128"));
	    Integer num4 = Integer.valueOf(128);

	    System.out.println(num1 == num2);
	    System.out.println(num1 == num3);
	    System.out.println(num1 == num4);
	    System.out.println("-----");

	    Integer num5 = new Integer(128);
	    System.out.println(num1 == num5);
	    System.out.println(num1.equals(num5));
	    System.out.println(num0 == num1.intValue());
	  }




可以看到, 编译器在将 int 值赋给 Integer 时，自动进行了 Integer.valueOf 包装。

而在将 Integer 转换为 int 时,使用的是 num1.intValue() 这种形式。


这就是 Java的自动包装/解包 机制。

很简单的语法糖,由编译器(javac)实现。

所以对 JVM 没什么影响, 在将 .java 文件编译为 .class 就已经处理完成。


具体实现:

使用的是 内部私有静态类:

    private static class IntegerCache {
	//...
    }

只有通过 valueOf 方法调用才生效:


    public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }


其他的 Number 包装类, 比如 Long, Short 等,其 valueOf 也使用了 cache 机制.
