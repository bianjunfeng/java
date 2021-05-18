# edu后续知识

# 1、抽象类里面的抽象方法

在抽象类中可以有构造方法，只是不能直接创建抽象类的实例对象，但实例化子类的时候，就会初始化父类，不管父类是不是抽象类都会调用父类的构造方法，初始化一个类，先初始化父类。

##### 接口和抽象类的语法区别：

```
1）接口不能有构造方法，抽象类可以有。
2）接口不能有方法体，抽象类可以有。
3）接口不能有静态方法，抽象类可以有。
4）在接口中凡是变量必须是public static final，而在抽象类中没有要求。
```



# 2、**String&StringBuilder&StringBuffer类-**

- [一、String类](https://www.cnblogs.com/zeo-to-one/p/9348237.html#一、string类)
- [二、"==" 和 “equals”的区别](https://www.cnblogs.com/zeo-to-one/p/9348237.html#二、--和-equals的区别)
- [三、StringBuffer和StringBuilder](https://www.cnblogs.com/zeo-to-one/p/9348237.html#三、stringbuffer和stringbuilder)



##### 一、String类

String为引用数据类型，final的，不可被继承。不可变的Unicode字符序列。本质上为char 字符数组

- 字符串方法

| 方法                                 | 含义                                           |
| ------------------------------------ | ---------------------------------------------- |
| int length()                         | 获取字符串的长度                               |
| int indexOf(int ch)                  | 返回指定字符在此字符串中第一次出现处的索引     |
| int indexOf(String str)              | 返回指定子字符串在此字符串中第一次出现处的索引 |
| int lastIndexOf(int ch)              | 返回指定字符在此字符串中最后一次出现处的索引   |
| int compareTo(Object o)              | 把这个字符串和另一个对象比较                   |
| String intern()                      | 返回字符串对象的规范化表示形式                 |
| String trim()                        | 去除字符串前后空格                             |
| String toLowerCase()                 | 将字符串全部转换为小写                         |
| String toUpperCase()                 | 将字符串全部转换为大写                         |
| String substring(int index)          | 按索引截取字符串                               |
| String substring(int begin, int end) | 指定索引范围截取字符串                         |
| String replace(char old, char new)   | 将新字符替换旧的字符                           |
| String[] split(String regex)         | 给定正则表达式的匹配拆分此字符串               |
| boolean matches(String regex)        | 符串是否匹配给定的正则表达式                   |
| boolean isEmpty()                    | 判断字符串的长度是否等于0                      |
| boolean equals(Object obj)           | 字符串与指定的对象比较                         |
| boolean equalsIgnoreCase(String str) | 判断两字符串比较(忽略大小写)                   |
| boolean startsWith(String prefix)    | 字符串是否以指定的前缀开始                     |
| boolean endsWith(String suffix)      | 字符串是否以指定的后缀结束                     |
| char[] toCharArray()                 | 字符串转换为一个新的字符数组                   |
| static String valueOf(type x)        | 将指定类型的参数转换为字符串类型               |

- 字符串连接
  String str="You and ".concat("Me");
  String str="You and " + "Me" + 'I';
  // 可连接字符串或者数字及其他基本类型数据； concat只接受字符串
  还可以使用StringBuffer或StringBuilder进行连接
- 格式化输出字符串
  printf() 和 format()
  浮点型为 %f ;整型为 %d ; 字符串为 %s
  例子：`String str=String.format("%f %d %s", 1.1, 5, "aa") ;`

字符串替换实例：

```java
// 字符串替换的方法
 String s = "one dog and two dogs ";
 System.out.println(s.replaceFirst("dog","cat"));//第一次匹配的字符替换为指定字符串
 System.out.println(s.replaceAll("one|two","three"));// 所有匹配替换为指定字符串
 System.out.println(s.replace("do","pi"));// 将目标字符串替换为指定字符串
 System.out.println(s.replace('a','A'));// 将旧字符 a 替换为新字符 A
```

##### 二、"==" 和 “equals”的区别

首先 **==** 是用来比较两个变量所指向的内存地址是否相同，可以用来两个基本类型的数据或两个引用变量是否相等。
在Object类中： equals方法的实现是 `return this==obj` , 也就是说equals与 == 是一样的，比较的都是两个对象所指向的内存地址是否相同。但是在String类中重写了父类Obejct中的equls方法，比较的是两个对象的内容是否相同。例子：

```java
 // final String s = "ab";
 String s = "ab"; // 栈中存放变量 s , String池中存放常量"ab", 变量s指定常量 "ab";
 String a = "abc"; // 在栈中开辟空间存放变量 a,String池中开辟空间存放"abc"，变量a指向String中的常量"abc";
 String b = "ab" + "c"; // 栈中存放变量 b, 通过编译器优化合并后的常量为 "abc";
 String c = "ab".concat("c"); // 如果传入的参数长度为大于0， 则返回一个new String(buf, true)对象,存放在堆中;
 String d = s + "c";// 栈中存放变量d , String池中存放常量"c", 运行后才能确定变量d的值(对象),存放在堆中。
                     // （通过StringBuilder的toString方法返回一个新的对象"adc"）, 变量d 指向这个新的对象。

 System.out.println(a==b); // true
 System.out.println(a==c); // false
 System.out.println(a==d); // false 如果变量s 被定义为final对象，则 a==d 结果为 true
 System.out.println(b==c); // false
 System.out.println(b==d); // false 如果变量s 被定义为final对象，则 b==d 结果为 true
 System.out.println(c==d); // false

 // a,b,c d 三个变量，也就是对象的内容都是"abc",所以都返回true
 System.out.println(a.equals(b)); // true
 System.out.println(a.equals(c)); // true
 System.out.println(a.equals(d)); // true
 System.out.println(b.equals(c)); // true
```

##### 三、StringBuffer和StringBuilder

StringBuffer和StringBuilder：每个字符串缓冲区都有一定的容量(初始容量为 16 个字符)。只要字符串缓冲区所包含的字符序列的长度没有超出此容量，就无需分配新的内部缓冲区数组。如果内部缓冲区溢出，则此容量自动增大。
从源码来看StringBuffer和StringBuilder都是继承抽象类AbstractStringBuilder，调用了父类的方法。StringBuffer调用的父类方法都有修饰符synchronized。

> StringBuffer 允许并发操作，线程安全
> StringBuilder 不支持并发操作，非线程安全；但速度更优

StringBuffer 类的常用方法：

| 方法                                    | 含义                               |
| --------------------------------------- | ---------------------------------- |
| append(String s)                        | 追加指定的字符串                   |
| reverse()                               | 反转字符串                         |
| delete(int start, int end)              | 删除指定index范围的字符，不包含end |
| insert(int offset, String str)          | 从指定位置插入字符串               |
| replace(int start, int end, String str) | 替换指定范围的字符串               |
| int capacity()                          | 返回容量大小                       |
| int length()                            | 返回长度（字符数）                 |
| void setLength(int newLen)              | 设置字符序列的长度                 |
| indexOf()/ substring()                  | 与String类一致                     |

实例：

> 字符串翻转

- 方法一

```java
  // 使用StringBuffer中自带的reverse方法(调用父类的reverse)
 String s = "1234";
 StringBuffer sb = new StringBuffer(s);
 System.out.println(sb.reverse()); // "4321"
```

- 方法二

```java
 // 使用for循环字符追加的方式
  String s = "1234",t="";
  for(int i=s.length()-1; i>=0 ;i--){
      t += s.charAt(i);
  }
  System.out.println(t); // "4321"
```

> 统计字符串中每个字符的个数

- 方法一

```java
// 使用StringBuilder去重，for遍历统计
String s = "hello word test is";
StringBuilder sb = new StringBuilder();
for(int i=0;i<s.length();i++){
    String ss = String.valueOf(s.charAt(i));
    if (sb.indexOf(ss)== -1) { //去重
        sb.append(ss);
        int t=0;
        for(int j=0; j<s.length();j++){
            if(s.charAt(j)==ss.charAt(0)){
                t++;
            }
        }
        System.out.println(ss+":"+t+"个");
    }
}
```

- 方法二

```java
// 对字符串重新排序，利用索引位置差进行统计
String s = "hello word test is";
char [] chars = s.toCharArray();
Arrays.sort(chars);
String ns = new String(chars); // 排序后的新字符串    deehilloorssttw
for(int i=0;i<s.length();){
    String ss = String.valueOf(ns.charAt(i));
    int index = ns.lastIndexOf(ss); // 字符最后的索引位置
    System.out.println(ss+": "+(index+1-i)+"个");
    i=index+1; //下一个字符的索引位置
}
```

- 方法三

```java
// 将重复的字符去除，利用字符串的长度统计
String s = "hello word test is";
while(s.length()>0){
    String ss = String.valueOf(s.charAt(0));
    String ns = s.replaceAll(ss,"");
    int t = s.length() - ns.length();
    s = ns;
    System.out.println(ss + ": " + t + "个");
}
```

- 方法四

```java
// 利用Map的key不能重复，进行统计
String s = "hello word test is";
 Map<Character, Integer> hm = new HashMap<Character, Integer>();
 for(int i=0; i<s.length();i++){
     char c = s.charAt(i);
     if(hm.containsKey(c)){
        hm.put(c,hm.get(c)+1);
     }else{
         hm.put(c,1);
     }
 }
 for(Entry<Character, Integer> e: hm.entrySet()){
     System.out.println(e.getKey()+": "+e.getValue()+ "个");
 }
```

# 3、包装类

##### 一.什么是包装类

　　![img](https://img2018.cnblogs.com/blog/1395687/201904/1395687-20190427100228249-1831265356.png)

　　Java中的基本数据类型没有方法和属性，而包装类就是为了让这些拥有方法和属性，实现对象化交互。

![img](https://img2018.cnblogs.com/blog/1395687/201904/1395687-20190427100603451-1800197804.png)

 数值型包装类都继承至Number，而字符型和布尔型继承至Object。

##### 二.基本数据和包装类之间的转换

　　装箱：基本数据类型转换为包装类；

 

　　拆箱：包装类转换为基本数据类型。　

![img](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```java
 1 package com.swpu;
 2 
 3 public class WrapperTestOne {
 4     public static void main(String[] args){
 5         //1.自动装箱
 6         int t1=1;
 7         Integer t2=t1;
 8         //2.手动装箱
 9         Integer t3=new Integer(t1);
10         System.out.println("int类型t1="+t1);
11         System.out.println("自动装箱，Integer类型对象t2="+t2);
12         System.out.println("手动装箱，Integer类型t3="+t3);
13         
14         
15         //1.自动拆箱
16         int t4=t2;
17         //2.手动拆箱
18             //通过intValue()方法返回int值，还可以利用其他方法装换为其他类型
19         int t5=t2.intValue();
20         System.out.println("自动拆箱,int型t4="+t4);
21         System.out.println("手动拆箱,int型t5="+t5);
22     }
23 
24 }
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

##### 三.基本数据类型和包装类的转换

　　通过包装类Integer.toString()将整型转换为字符串；

　　通过Integer.parseInt()将字符串转换为int类型；

　　通过valueOf()方法把字符串转换为包装类然后通过自动拆箱。

![img](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```java
 1 package com.swpu;
 2 
 3 public class WrapperTestTwo {
 4 
 5     public static void main(String[] args) {
 6         // TODO Auto-generated method stub
 7         //基本数据类型转换为字符串
 8         int t1=12;
 9         String t2=Integer.toString(t1);
10         System.out.println("int转换为String："+t2);
11         //字符串转换为基本数据类型
12         //通过paerInt方法
13         int t3=Integer.parseInt(t2);
14         //通过valeOf,先把字符串转换为包装类然后通过自动拆箱
15         int t4=Integer.valueOf(t2);
16         System.out.println("t3:"+t3);
17         System.out.println("t4:"+t4);
18 
19     }
20 
21 }
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

##### 四.包装类知识

　　包装类对象的初始值为null（是一个对象）；

　　包装类对象之间的比较：

![img](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```java
 1 package com.swpu;
 2 
 3 public class WrapperTestTre {
 4 
 5     public static void main(String[] args) {
 6         // TODO Auto-generated method stub
 7         Integer one=new Integer(100);
 8         Integer two=new Integer(100);
 9         //one和对two是两个不同的对象，==在比较对象时比较的是内存地址，两个是不同的空间，放的值相同
10         System.out.println("one==two:"+(one==two));
11         Integer three=100;//自动装箱
12         /*    Integer three=Integer.valueOf(100);
13          * 这时缓存区没有，就会构造一个
14          */
15         System.out.println("three==100:"+(three==100));//自动拆箱
16         Integer four=100;
17         /*实际执行的是    Integer four=Integer.valueOf(100); 这时缓存区有，就会直接取
18          * Java为了提高拆装箱效率，在执行过程中提供了一个缓存区（对象池）【类似于常量数组】，
19          * 如果传入的参数是，-128<参数<127会直接去缓存查找数据，如果有久直接产生，如果没有就隐式调用new方法产生
20          */
21         
22         System.out.println("three==four:"+(three==four));
23         Integer five=200;
24         System.out.println("five==200:"+(five==200));
25         Integer six=200;
26         //注：这里为200，超出了缓存区范围，所以都需要构建
27         System.out.println("five==six:"+(five==six));
28         /*
29          * 输出：
30          *     one==two:false
31             three==100:true
32             three==four:true
33             five==200:true
34             five==six:false
35 
36          */
37     }
38 
39 }
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

　　注：

　　　　Java中除了float和double的其他基本数据类型，都有常量池（注：Python中int【-5~256，257 这个整数对象是区分作用域的，它只有在相同的作用域, 内存地址才会相同

】,str,byte也有

5、Math类

```java
static double abs(double a)

返回 double 值的绝对值。

static float abs(float a)

返回 float 值的绝对值。

static int abs(int a)

返回 int 值的绝对值。

static long abs(long a)

返回 long 值的绝对值。

static double acos(double a)

返回角的反余弦，范围在 0.0 到 pi 之间。

static double asin(double a)

返回角的反正弦，范围在 -pi/2 到 pi/2 之间。

static double atan(double a)

返回角的反正切，范围在 -pi/2 到 pi/2 之间。

static double atan2(double y, double x)

将矩形坐标 (x, y) 转换成极坐标 (r, theta)。

static double cbrt(double a)

返回 double 值的立方根。

static double ceil(double a)

返回最小的（最接近负无穷大）double 值，该值大于或等于参数，并且等于某个整数。

static double cos(double a)

返回角的三角余弦。

static double cosh(double x)

返回 double 值的双曲线余弦。

static double exp(double a)

返回欧拉数 e 的 double 次幂的值。

static double expm1(double x)

返回 ex -1。

static double floor(double a)

返回最大的（最接近正无穷大）double 值，该值小于或等于参数，并且等于某个整数。

static double hypot(double x, double y)

返回 sqrt(x2 +y2)，没有中间溢出或下溢。

static double IEEEremainder(double f1, double f2)

按照 IEEE 754 标准的规定，对两个参数进行余数运算。

static double log(double a)

返回（底数是 e）double 值的自然对数。

static double log10(double a)

返回 double 值的底数为 10 的对数。

static double log1p(double x)

返回参数与 1 的和的自然对数。

static double max(double a, double b)

返回两个 double 值中较大的一个。

static float max(float a, float b)

返回两个 float 值中较大的一个。

static int max(int a, int b)

返回两个 int 值中较大的一个。

static long max(long a, long b)

返回两个 long 值中较大的一个。

static double min(double a, double b)

返回两个 double 值中较小的一个。

static float min(float a, float b)

返回两个 float 值中较小的一个。

static int min(int a, int b)

返回两个 int 值中较小的一个。

static long min(long a, long b)

返回两个 long 值中较小的一个。

static double pow(double a, double b)

返回第一个参数的第二个参数次幂的值。

static double random()

返回带正号的 double 值，大于或等于 0.0，小于 1.0。

static double rint(double a)

返回其值最接近参数并且是整数的 double 值。

static long round(double a)

返回最接近参数的 long。

static int round(float a)

返回最接近参数的 int。

static double signum(double d)

返回参数的符号函数；如果参数是零，则返回零；如果参数大于零，则返回 1.0；如果参数小于零，则返回 -1.0。

static float signum(float f)

返回参数的符号函数；如果参数是零，则返回零；如果参数大于零，则返回 1.0；如果参数小于零，则返回 -1.0。

static double sin(double a)

返回角的三角正弦。

static double sinh(double x)

返回 double 值的双曲线正弦。

static double sqrt(double a)

返回正确舍入的 double 值的正平方根。

static double tan(double a)

返回角的三角正切。

static double tanh(double x)

返回 double 值的双曲线余弦。

static double toDegrees(double angrad)

将用弧度测量的角转换为近似相等的用度数测量的角。

static double toRadians(double angdeg)

将用度数测量的角转换为近似相等的用弧度测量的角。

static double ulp(double d)

返回参数的 ulp 大小。

static float ulp(float f)

返回参数的 ulp 大小。
```

# 4、Object类

1.什么是`Object`类；

2.`Object`类的方法；

3.`Java`对象克隆。

##### 什么是`Object`类

`Java`中有一个比较特殊的类，就是 `Object `类，它是所有类的父类，如果一个类没有使用`extends`关键字明确标识继承另外一个类，那么这个类就默认继承 `Object `类。因此，`Object `类是 Java 类层中的最高层类，是所有类的超类。换句话说，Java 中任何一个类都是它的子类。由于所有的类都是由 `Object `类衍生出来的，所以 `Object `类中的方法适用于所有类。

```
public class Person //当没有指定父类时,会默认 Object 类为其父类{
...
}
```

上面的程序等价于：

```
public class Person extends Object{
...
}
```

如果想引用你不知道的类型的对象，使用`Object`类是没有错的。请注意，父类引用变量可以引用子类对象，称为向上转换。下面举一个例子，有一个`getObject()`方法返回一个对象，但它可以是任何类型，如：`Employee`，`Student`等这样的类，我们可以使用`Object`类引用来引用该对象。 例如：

```
Object obj=getObject();//we don't know what object will be returned from this method
```

`Object`类为所有对象提供了一些常见的行为，如对象可以进行比较，对象可以克隆，对象可以通知等。

![img](https://data.educoder.net/api/attachments/207853) 

##### `Object`类的方法

`Object`类提供了许多方法。 它们如下：

![img](https://data.educoder.net/api/attachments/206847) 

`Object`类的常用方法有： `toString()`和`equals()`方法。

1.关于`toString()`方法

- 在`Object`类里面定义`toString()`方法的时候返回的对象的哈希`code`码(对象地址字符串)；
- 可以通过重写`toString()`方法表示出对象的属性。

此方法是在打印对象时被调用的，下面有两个范例，一个是没复写`toString()`方法，另一个是复写了` toString()`方法，读者可比较两者的区别。

```java
package educoder;public class TestToStringDemo1 {
public static void main(String[] args) {
	Person p = new Person();
    System.out.println(p);
    }
}
class Person extends Object {
	String name = "张三";
	int age = 18;}
```

输出结果： `educoder.Person@7852e922`

2.关于`equals()`方法 



`equals()` 和` ==` 的区别：

- 在Java中，任何类型的数据都可以用 “==”进行比较是不是相等，一般用于基本数据类型的比较，比较器存储的值是否相等。但是如果用于引用类型的比较，则是比较所指向对象的地址是否相等，在这点上，跟`object`类提供的`equals()`方法的作用是一致的。
- 对于`equals()`方法

1. 首先，不能用于基本数据类型的变量之间的比较相等；
2. 如果没有对`equals`方法进行重写，则比较的是引用类型的变量所指向的对象的地址；
3. 诸如`String`、`Date`等类都对`equals`方法进行了重写，比较的是所指向的对象的内容。

##### Java对象克隆

对象克隆是一种创建对象的精确副本的方法。` Object`类的`clone()`方法用于克隆对象。`java.lang.Cloneable`接口必须由我们要创建其对象克隆的类实现。如果我们不实现`Cloneable`接口，`clone()`方法将生成`CloneNotSupportedException`。

`clone()`方法在`Object`类中定义。 `clone()`方法的语法如下：

```
protected Object clone() throws CloneNotSupportedException
```

为什么要使用`clone()`方法？

`clone()`方法保存用于创建对象的精确副本的额外处理任务。 如果我们使用`new`关键字执行它，它将需要执行大量的处理，这就是为什么我们使用对象克隆。 对象克隆的优点：

- 少处理任务。



