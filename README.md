# Java入门


## 1.Java入口函数

> Test1.java

	public class Test1 {
	    public static void main(String[] args){
	    }
	}


## 2. 基本静态方法

> Test2.java

	public class Test2 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	    }
	}


## 3. 打印到控制台

> Test3.java

	public class Test3 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        System.out.println("第0个数字:" + 0);
	    }
	}


## 4. 打印多个记录

> Test4.java

	public class Test4 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        System.out.println("第0个数字:" + 0);
	        System.out.println("第1个数字:" + 1);
	        System.out.println("第2个数字:" + 2);
	        System.out.println("第3个数字:" + 3);
	        System.out.println("第4个数字:" + 4);
	        System.out.println("第5个数字:" + 5);
	        System.out.println("第6个数字:" + 6);
	        System.out.println("第7个数字:" + 7);
	        System.out.println("第8个数字:" + 8);
	        System.out.println("第9个数字:" + 9);
	    }
	}

## 5. 基本循环

> Test5.java

	public class Test5 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        for (int i = 0; i < 10; i++){
	            System.out.println("第"+ i +"个数字:" + i);
	        }
	    }
	}

## 6. 使用中间变量

> Test6.java

	public class Test6 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        int n = 20;
	        for (int i = 0; i < n; i++){
	            System.out.println("第"+ i +"个数字:" + i);
	        }
	    }
	}

## 7. while 等价循环

> Test7.java

	public class Test7 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        int n = 20;
	        int i = 0;
	        while (i < n){
	            System.out.println("第"+ i +"个数字:" + i);
	            i++;
	        }
	    }
	}


## 8. 取模/求余数

> Test8.java

	public class Test8 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        int n = 10000;
	        for (int i = 0; i < n; i++){
	            if(0 == i % 100){
	                System.out.println("第"+ i +"个数字:" + i);
	            }
	        }
	    }
	}


## 9. 提取中间变量,常量

> Test9.java


	public class Test9 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        final int n = 100000;
	        final int mod = 1000;
	        for (int i = 0; i < n; i++){
	            if(0 == i % mod){
	                System.out.println("第"+ i +"个数字:" + i);
	            }
	        }
	    }
	}



## 10. 累加

> TestAdd1.java

	public class TestAdd1 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        final int n = 100;
	        int sum = 0;
	        for (int i = 0; i < n; i++){
	            //
	            sum = sum + i;
	        }
	        // 4950
	        System.out.println("0-"+ n +"个数字的和为:" + sum);
	    }
	}


## 11. 注意起始数字以及边界

> TestAdd2.java


	public class TestAdd2 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        final int n = 100;
	        int sum = 0;
	        for (int i = 1; i <= n; i++){
	            //
	            sum = sum + i;
	        }
	        // 5050
	        System.out.println("1-"+ n +"的和为:" + sum);
	    }
	}


## 12. 提取公共逻辑

> TestAdd3.java

	public class TestAdd3 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        final int n = 100;
	        final int allNum = 1000;
	        sum(n);
	        sum(allNum);
	    }
	
	    public static void sum(int n){
	        int sum = 0;
	        for (int i = 1; i <= n; i++){
	            //
	            sum = sum + i;
	        }
	        System.out.println("1-"+ n +"的和为:" + sum);
	    }
	}


## 13. 公共逻辑不处理交互

> TestAdd4.java

	public class TestAdd4 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        final int n = 100;
	        final int allNum = 1000;
	
	        int sumN =  sum(n);
	        System.out.println("1-"+ n +"的和为:" + sumN);
	
	        int sumAllNum =  sum(allNum);
	        System.out.println("1-"+ allNum +"的和为:" + sumAllNum);
	
	    }
	
	    public static int sum(int n){
	        int sum = 0;
	        for (int i = 1; i <= n; i++){
	            //
	            sum = sum + i;
	        }
	        return sum;
	    }
	}


## 14. int 整型溢出

> TestAdd5.java

	public class TestAdd5 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        final int n = 10000 * 40;
	        // java 中 int,4字节= 2^32次方 ~= 40多亿.
	        // 刨除一半负数,已经存放不下: 30亿
	        // 整型溢出, -1294967296
	        final int allNum = 10000 * 10000 * 30;
	
	        // int 也存放不下1到40万的和,得到一个负数,明显是溢出了。
	        int sumN =  sum(n);
	        // 1-400000的和为:-1604178624
	        System.out.println("1-"+ n +"的和为:" + sumN);
	
	        int sumAllNum =  sum(allNum);
	        // 1- -1294967296的和为:0
	        System.out.println("1-"+ allNum +"的和为:" + sumAllNum);
	
	    }
	
	    public static int sum(int n){
	        int sum = 0;
	        for (int i = 1; i <= n; i++){
	            //
	            sum = sum + i;
	        }
	        return sum;
	    }
	}


## 15. 改为 long 类型

> TestAdd6.java

	public class TestAdd6 {
	    public static void main(String[] args){
	        test();
	    }
	    public static void test(){
	        // ...
	        final long n = 10000 * 40;
	        // 此处在编译期就已经出问题了
	        final long allNum = 10000 * 10000 * 30;
	
	        long sumN =  sum(n);
	        // 1-400000的和为:80000200000
	        System.out.println("1-" + n + "的和为:" + sumN);
	
	        long sumAllNum =  sum(allNum);
	        // ??? 怎么回事
	        // 1- -1294967296的和为:0
	        System.out.println("1-"+ allNum +"的和为:" + sumAllNum);
	
	    }
	
	    public static long sum(long n){
	        long sum = 0;
	        for (long i = 1; i <= n; i++){
	            sum = sum + i;
	        }
	        return sum;
	    }
	}


## 16. 修正编译期的类型错误

> TestAdd7.java

	public class TestAdd7 {
	    public static void main(String[] args){
	        long startTimestamp = System.currentTimeMillis();
	        test();
	        long endTimestamp = System.currentTimeMillis();
	        //总共耗时: 1859 毫秒.
	        System.out.println("总共耗时: " + (endTimestamp - startTimestamp) + " 毫秒.");
	    }
	    public static void test(){
	        // ...
	        final long n = 10000 * 40;
	        // 如果不加 L 标识,则在编译期就隐含了错误
	        final long allNum = 10000L * 10000 * 30;
	
	        long sumN =  sum(n);
	        // 1-400000的和为:80000200000
	        System.out.println("1-" + n + "的和为:" + sumN);
	
	        long sumAllNum =  sum(allNum);
	        // 1-3000000000的和为:4500000001500000000
	        System.out.println("1-"+ allNum +"的和为:" + sumAllNum);
	
	    }
	
	    public static long sum(long n){
	        long sum = 0;
	        for (long i = 1; i <= n; i++){
	            sum = sum + i;
	        }
	        return sum;
	    }
	}

> 30亿次数学运算,对现代CPU并没有什么压力. 1GHZ ~= 10亿次运算每秒.


## 17. 使用 BigInteger计算大整数

如果数字更大,超过 40亿 * 40亿 这个级别，则long类型也存放不下。

> TestAdd8.java

	public class TestAdd8 {
	    public static void main(String[] args){
	        long startTimestamp = System.currentTimeMillis();
	        test();
	        long endTimestamp = System.currentTimeMillis();
	        System.out.println("总共耗时: "+ (endTimestamp - startTimestamp) +" 毫秒.");
	        // 总共耗时: 188625 毫秒.
	    }
	    public static void test(){
	        // ...
	        final Long allNum = 10000L * 10000 * 30;
	        final BigInteger allNumInteger = new BigInteger(allNum.toString());
	
	        BigInteger sumAllNum =  sum(allNumInteger);
	        // 1-3000000000的和为:4500000001500000000
	        System.out.println("1-"+ allNum +"的和为:" + sumAllNum);
	    }
	
	    public static BigInteger sum(BigInteger n){
	        BigInteger sum = new BigInteger("0");
	        BigInteger ONE = new BigInteger("1");
	        BigInteger i = new BigInteger("1");
	        while (n.compareTo(i) > -1){
	            sum = sum.add(i);
	            i = i.add(ONE);
	        }
	        return sum;
	    }
	}

耗时 180秒, 对比上面的 long 类型示例的运行时间 1.8 秒。可以得出 BigInteger 的运算性能比 long 要低很多。

粗略算是100倍的差距，但不可武断地依赖这个数字。虽然是100倍,但常规业务中一般不会涉及到这么多量的计算。

180秒,如果是在线业务处理,估计客户早就放弃了。


## 18. 改进 sum 算法

我们知道高斯总结了一个公式。 据说是他小时候就搞定了的。

	sum(n) = n(n+1)/2

