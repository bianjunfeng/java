~~~java
1、素数
package com.liuhuan.java;

public class PrimeNumberMethod {

```
/**
 * 把该问题分解成确定素数以及打印出素数
 * */
public static void main(String[] args) {
	System.out.println("The first 50 prime numbers are \n");
	printPrimeNumber(50);

}

/** 打印素数 */
public static void printPrimeNumber(int numberOfPrime){
	final int NUMBER_OF_PRIME_PER_LINE = 10;
	int count = 0;
	int number = 2;
	while(count < numberOfPrime){
		if(isPrime(number)){
			count++;
			// 每10个换一行打印
			if(count % NUMBER_OF_PRIME_PER_LINE == 0){
				System.out.printf("%-5s\n", number);//格式化打印
			}else{
				System.out.printf("%-5s", number);
			}
		}
		number++;
	}
	
}

/** 判断是否为素数 */
public static boolean isPrime(int number){
	for(int divisor = 2; divisor <= number / 2; divisor++){
		if(number % divisor == 0){
			return false;
		}
	}
	return true;
}
```

}
2、回文数
package d0225;

public class HuiWen {
    public static boolean huiwen(int n){
        String str= String.valueOf(n);
        int length = str.length();
        int a=0;
        for(int i=0;i<length/2;i++){
            if (str.charAt(i)==str.charAt(length-i-1)){
                a++;
            }
        }
        return a==str.length()/2;
    }
    public static boolean huiwen2(int n){
        String str= String.valueOf(n);
        int length = str.length();
        boolean flag=false;
        for(int i=0;i<length/2;i++){
            if (str.charAt(i)==str.charAt(length-i-1)){
                flag=true;
            }else {
                return false;
            }
        }
        return flag;
    }

    public static void main(String[] args) {
        int a=123321;
        int b=123696321;
        int c=1233219;
        System.out.println(huiwen(a));
        System.out.println(huiwen(b));
        System.out.println(huiwen(c));
        System.out.println(huiwen2(a));
        System.out.println(huiwen2(b));
        System.out.println(huiwen2(c));
    }
}
3、多线程水仙花数
package test1;

public class ThreadeExam {
    public static void main(String[] args) {
        Thread th1 = new Thread(new Runnable() {
            @Override
            public void run() {
                int sum = 0;
                for (int i = 0; i < 1000; i++)
                    sum+=i;
                    System.out.println("sum"+sum);

            }
        });
        Thread th2 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 100; i < 1000; i++) {
                    String tempStr = Integer.toHexString(i);
                    int x = Integer.parseInt(tempStr.substring(0,1));
                    int y = Integer.parseInt(tempStr.substring(1,2));
                    int z = Integer.parseInt(tempStr.substring(2,3));
                    if(i==x*x*x+y*y*y+z*z*z)
                        System.out.println("The flower number:"+i);
                }
            }
        });
            th1.start();
            th2.start();
    }
}
4、阶乘之和
package experiment.test1;
//(1)编写应用程序, 求一个自然数N的阶乘。。
import java.util.*;
public class homeWork1 {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入要算的数：");
        int n = sc.nextInt();
        System.out.println(new homeWork1().jieChen(n));
    }

    public static int jieChen(int a) {
        int sum = 1;
        for (int i =a; i> 0; i--) {

            sum = a * sum;

        }
        return sum;


    }
}


5、排序
public class xuanze{
    public static void main(String[] args) {
        int[] arr = {24,69,80,57,13};
        selectSort(arr);
    }

    public static void selectSort(int[] arr) {

        for(int i = 0; i < arr.length-1; i++) {

            for (int j = i+1; j < arr.length; j++) {

                if(arr[i] > arr[j]) {
                    int tmp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = tmp;
                }
            }
        }

        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
public class maopao {
    public static void main(String[] args) {
        int[] a = {13, 213, 421, 34};
        //first method
        for (int i = 0; i <a.length; i++) {
            for (int j = 0; j < a.length-i-1; j++) {
                if (a[j] > a[j + 1]) {
                    int temp;
                    temp = a[j];
                    a[j] = a[j + 1];
                    a[j + 1] = temp;
                }
            }
            }
        //second method
        for(int i =a.length-1;i>0;i--){
            for (int j =0;j<i;j++){
                if(a[j]>a[j+1]){
                int temp;
                temp = a[j];
                a[j]=a[j+1];
                a[j+1]=temp;
                }
            }
        }
        for (int i = 0; i <a.length; i++) {
                System.out.println(a[i]);
        }
    }
}

6、字符串的split拆分
 public static void main(String[] args) {
        String str = "I Live In The Home";
        String[] ret = str.split(" ");
        for (String x : ret){
            System.out.println(x);
        }
        System.out.println("原来的字符串为：" + str);
        //System.out.println(Arrays.toString(ret));
    }

7、字符串和数字的转换

给定一个字符串 String str = "1234";

转为转数字 1234：

valueOf()

int  num = Integer.valueOf(str);

parseInt()

int num = Integer.parseInt(s);	

8、奇偶数
import java.util.Scanner;
public class ParityCheck {//类
    public static void main(String[] args) {//主方法
        Scanner scan = new Scanner(System.in);//扫描器
        System.out.println("Please input Integer:");
        long A = scan.nextLong();//接收变量值
        if(A%2 == 0){
            System.out.println("这个数字是偶数");
        }else{
            System.out.println("这个数字是奇数");
        }
    }
}

~~~

