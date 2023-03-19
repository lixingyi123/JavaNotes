<p align = "center" ><font size = 6， color = "#009999">String & StringBuilder & ArrayList</font></p>

## 1、String

```java
public final class String extends Object implements Serializable, Comparable<String>, CharSequence
```

`String`类代表字符串。Java程序中的所有字符串文字（例如`"abc"` ）都被实现为此类的实例。

Java程序中所有用双引号`" "`括起来的字符串，都是String类的对象。

字符串是不变的; 它们的值在创建后不能被更改。字符串缓冲区支持可变字符串。  因为String对象是用final修饰的（不可变的），它们可以被共享。 例如： 

```java
String str = "abc";

// 相当于

char data[] = {'a', 'b', 'c'};
String str = new String(data);
```

### 1.1 String类构造方法

```java
String() 
    初始化一个新创建的 String 对象，使其表示一个空字符序列。
    
String(char[] value) 
    分配一个新的 String，使其表示字符数组参数中当前包含的字符序列。
    
String(char[] value, int offset, int count) 
	分配一个新的 String ，其中包含字符数组参数的子阵列中的字符。 
    
String(byte[] bytes) 
    通过使用平台的默认字符集解码指定的 byte 数组，构造一个新的 String。
 
String(byte[] bytes, int offset, int length) 
	通过使用平台的默认字符集解码指定的字节子阵列来构造新的 String 。 
    
String = "abc"；
```

```java
public class Test{
    public static void mian(String[] args){
        // 创建一个空字符序列
        String str1 = new String();
        System.out.println("=" + str1 + ",");
        
        // 根据字符char数组来创建String
        // String(char[] value)
        char[] char1 = {'a', 'b', 'c', 'd', 'e'};
        String str2 = new String(char1);
        System.out.println(str2);// abcde
        
        //String(char[] value, int offset, int count)
        System.out.println(new String(char1, 1, 3)); // bcd
        
        // 根据字节数组的内容创建String
        // String(byte[] value)
        byte[] byte1 = {97, 98, 99, 100, 101, 102};
        String str3 = new String(byte1);
        System.out.println(str3); // abcdef
        
        // String(byte[] value, int offset, int length)
        System.out.println(new String(byte1, 1, 4));//bcde
        
        // 直接赋值创建字符串
        String str4 = "1233aad";
        System.out.println(str4); // 1233aad
    }
}
```

### 1.2 创建字符串的方式区别

#### 1.2.1 通过构造方法创建

通过构造方法创建时，**通过new创建的字符串对象，每次new都会申请一个堆空间， 内容相同，地址值不同**

```java
char[] char1 = {'a', 'b', 'c', 'd'};
String str1 = new String(char1);
String str2 = new String(char1);

// str1 与str2的地址值不同
```

#### 1.2.2 直接赋值的方式

通过直接=赋值的方式创建String。只要字符序列相同（顺序和大小写），无论在程序中出现多少次，JVM都只会创建一个String对象，并在字符串池中维护

```java
String str1 = "123adf";
String str2 = "123adf";

// 上述的str1与str2是一样的，首先，对于第一行代码，JVM只会创建一个String对象放在字符池中，并给str1参考。对于第二行代码，则直接让str2去参考字符串池中String对象，本质上是同一个对象
```

```java
public class Test{
    public static void main(String[] args){
        
        char[] chs = {'1', 'a', 'b', 'c'};
        String str1 = new String(chs);
        String str2 = new String(chs);
        
        System.out.println(str1 == str2); // false
        
        String str3 = "123add";
        String str4 = "123add";
        System.out.println(str3 == str4); // true
    }
}
```

### 1.3 String的特点

String类的字符串不可变，它的值在创建后就不可更改

```java
String str1 = "abc";
str1 += "d";
System.out.println(str1);

// 值没有变，改变的是指向
// str1从指向abc改为指向abcd
```

String在效果上相当于字符数组

```java
String str = "abc";

// 相当于

char data[] = {'a', 'b', 'c'};
String str = new String(data);
// String底层靠字符数组实现，jdk底层是字节数组
```

### 1.4 字符串的比较

#### 1.4.1 == 比较

1. 比较基本数据类型，比较的是具体的值
2. 比较引用数据类型，比较的是对象的地址值

#### 1.4.2 equals方法的比较

##### 1.4.2.1 方法介绍

```java
public boolean equals(Object s);
	比较两个字符串内容是否相同，区分大小写
boolean equalsIgnoreCase(String anotherString) 
	将此 String与其他 String比较，不区分大小写
        
System.out.println("a".equals("A")); // false

System.out.println("a".equalsIgnoreCase("A")); // true
```

**注意：**

**比较字符串内容是否相等，区分大小写，使用String类equals方法，不要用==比较**

不区分大小写，**使用equalsIgnoreCase（）**

### 1.5 String常用方法

```java
int length() 
      返回此字符串的长度。
    
String concat(String str) 
      将指定字符串连接到此字符串的结尾。 
    
char charAt(int index) 
      返回指定索引处的 char 值。 
    
int indexOf(String str) 
      返回指定子字符串在此字符串中第一次出现处的索引。 
    
int indexOf(String str, int fromIndex) 
      返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。 
    
int lastIndexOf(String str) 
      返回指定子字符串在此字符串中最右边出现处的索引。 
    
int lastIndexOf(String str, int fromIndex) 
      返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索。
    
String substring(int beginIndex) 
      返回一个新的字符串，它是此字符串的一个子字符串。 从beginIndex之后的字符串
    
String substring(int beginIndex, int endIndex) 
      返回一个新字符串，它是此字符串的一个子字符串。 
```

```java
public calss Test{
    public static void main(String[] args){
        String str1 = "Hello-good-Hello-good";
        // length
        System.out.println(str1.length()); // 21
        
        // str1尾部拼接
        String str2 = "Good";
        System.out.println(str1.concat(str2)); // Hello-good-Hello-goodGood
        
        // 获取str1中索引的值
        char ch = str1.charAt(2);
        System.out.println(ch); // l
        
        System.out.println("===============");
        
        // 查找Hello第一次出现位置的索引
        int index = str1.indexOf("Hello");
        System.out.println(index); // 0
        System.out.println(str1.indexOf("Hello", index + 1));// 11
        
        // 从右开始查找子字符串
        System.out.println(str1.lastIndexOf("Hello")); // 11
        
        // 获取str3的子字符串
        System.out.println(str1.substring(5)); // -good-Hello-good
        
        System.out.println(str1.substring(6, 14)); // good-Hel
        
    }
}
```

### 1.6 练习

#### 1.6.1 用户登录练习

已知用户名和密码，请用程序模拟用户登录，总共三次机会，登录之后给出相应提示

```java
import java.util.Scanner;

public class Test{
    public static void main(String[] args){
        String userName = "admin";
        String password = "123abc";
        
        Scanner sc = new Scanner(System.in);
        
        for (int i = 1; i <= 3; i++){
            System.out.println("请输入用户名：");
            String name = sc.next();
            
            System.out.println("请输入密码：");
            String pw = sc.next();
            
            if (name.equals(userName) && pw.equals(password)){
                System.out.println("登录成功,进入系统");
                break;
            } else{
                if (i == 3){
                    System.out.println("输入错误，你的账户已锁定，请联系管理员");
                } else {
                    System.out.println("账户名或密码输入错误，你还有" + (3 - i) + "次机会");
                }  
            }
             
        }
        sc.close();
    }
}
```

#### 1.6.2 遍历字符串

```java
import java.util.Scanner;

public class Test{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一串字符串：");
        String str = sc.next();
        // 遍历字符串
        for (int i = 0; i < str.length(); i++){
            System.out.pritnln(str.charAt(i));
        }
            
    }
}
```

#### 1.6.3 统计字符串的数量

键盘录入一个字符串，统计该字符串中大写字母，小写字母，数字字符出现的次数（不考虑其它字符）

统计实现：

1.大写字母：str >='A'  && str  <= 'Z'

2.小写字母：str >='a'  && str  <= 'z'

3.数字：str >='0'  && str  <= '9'

```java
import java.util.Scanner;

public class Test{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一串字符串：");
        String str = sc.next();
        
        int num = 0;
        int upperNum = 0;
        int lowerNum = 0;
        
        for (int i = 0; i < str.length(); i++){
            char ch = str.charAt(i);
            if (ch >= 'a' && ch <= 'z'){
                lowerNum++;
            }else if (ch >= 'A' && ch <= 'Z'){
                upperNum++;
            }else if (ch >= '0' && ch <= '9'){
                num++;
            }
        }
        System.out.println("数字有：" + num + "个");
        System.out.println("大写字母有：" + upperNum + "个");
        System.out.println("小写字母有：" + lowerNum + "个");
        sc.close();   
    }
}
```

#### 1.6.4 字符串反转

字符串反转：定义一个方法实现字符串反转。

键盘录入一个字符串，调用该方法，实现字符串反转：例如  键盘录入：abc，输出结果cba

```java
import java.util.Scanner;

public class Test{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一串字符串：");
        String str = sc.next();
        System.out.println(reverseStr(str));
        sc.close();
    }
    
    // 定义字符串反转方法
    public static String reverseStr(String str){
        String newStr = "";
        for (int i = str.length() - 1; i >= 0; i--){
            newStr += str.charAt(i);
        }
        return newStr;
    }
}
```

### 1.7 扩展String的方法

```java
boolean contains(CharSequence s) 
	当且仅当此字符串包含指定的char值序列时才返回true。 
    
boolean endsWith(String suffix) 
	测试此字符串是否以指定的后缀结尾。  

// 将字符串转换为字节数组
byte[] getBytes() 
	将String编码为字节序列，将结果存储到新的字节数组中。  

// 将字符串转换为字符数组
char[] toCharArray() 
	将字符串转换为字符数组,将结果存储到新的字符数组中 
    
boolean isEmpty() 
	返回 true如果，且仅当 length()为 0 。  
   
String replace(char oldChar, char newChar) 
	返回从替换所有出现的导致一个字符串 oldChar在此字符串 newChar 。
    
String[] split(String regex) 
	将此字符串分割为给定的 regular expression的匹配。  
    
boolean startsWith(String prefix) 
	测试此字符串是否以指定的前缀开头。
    
String toLowerCase() 
	将所有在此字符 String使用默认语言环境的规则，以小写。  
  

String toUpperCase() 
	将所有在此字符 String使用默认语言环境的规则大写。  

// 移除首尾的空格
String trim() 
	返回一个字符串，其值为此字符串，并删除任何前导和尾随空格。 
```

```java
public class Test{
    public static void main(String[] args){
       // 判断字符串是否为空
	        String str1 = "Hello-Good-Hello-Good";
	        System.out.println(str1.isEmpty()); // false
	        
	        // 判断字符串是否包含某个子字符串
	        System.out.println(str1.contains("hell0")); // false
	        System.out.println(str1.contains("Hello")); // true
	        
	        // 判断字符串是否以XX开头或结尾
	        System.out.println(str1.startsWith("He")); // true
	        System.out.println(str1.endsWith("oo")); // false
	        
	        // endsWith在开发中用来判断文件的类型
	        String file = "xxxxxxx.java";
	        System.out.println("判断上述文件是否是java文件:" + file.endsWith(".java"));
	        
	        
	        // 将Hello替换为hello
	        System.out.println(str1.replace("Hello", "hello")); // hello-Good-hello-Good
	        
	        // 将str1全部转换为大写/小写
	        System.out.println(str1.toUpperCase());
	        System.out.println(str1.toLowerCase());
	        
	        // 将字符串转换为字符数组
	        char[] arr = str1.toCharArray();
	        System.out.println(Arrays.toString(arr)); 
	        // [H, e, l, l, o, -, G, o, o, d, -, H, e, l, l, o, -, G, o, o, d]
	        
	        
	        // 将字符串转换为字节数组
	        byte[] arr2 = str1.getBytes();
	        System.out.println(Arrays.toString(arr2));
	        // [72, 101, 108, 108, 111, 45, 71, 111, 111, 100, 45, 72, 101, 108, 108, 111, 45, 71, 111, 111, 100]
	        
	        // 删除首尾的空格
	        String str2 = "   Hello    ";
	        System.out.println(str2.trim()); // Hello
	        
	        
	        // split分割，结果返回为数组
	        String[] str3 = str1.split("-");
	        System.out.println(Arrays.toString(str3)); // [Hello, Good, Hello, Good]
    }
}
```

## 2、StringBuilder

如果对String字符串进行拼接，每次拼接都会创建一个新的String对象，耗时有费空间

所以为了解决这个问题，可以使用java.lang.StringBuilder类

### 2.1 StringBuilder与String区别

1. String被final修饰，不可变
2. StringBuilder内容是可变的

### 2.2 构造方法

```java
StringBuilder() 
	构造一个没有字符的字符串构建器，初始容量为16个字符。  

StringBuilder(String str) 
	构造一个初始化为指定字符串内容的字符串构建器。  
```

```java
public class Test{
    public static void main(String[] args){
        StringBuilder sb1 = new StringBuilder();
        System.out.println("=" + sb1 + "="); // ==
        System.out.println(sb1.length()); // 0
        
        
        StringBuilder sb2 = new StringBuilder("123abc");
        System.out.println(sb2); // 123abc
    }
}
```

### 2.3 StringBuilder与String相互转换

#### 2.3.1 String转换为StringBuilder

直接通过StringBuilder构造方法转换

> StringBulider(String str)

#### 2.3.2 StringBuilder转换为String

```java
String toString()
	返回此序列中数据的字符串表示形式

StringBuilder sb = new StringBuilder("123abc");
// StringBuilder转换为String
String str = sb.toString();
```

### 2.4 StringBuilder类拼接与反转的方法

```java
StringBuilder append(任意类型) 
    将 boolean 参数的字符串表示形式追加到序列。 

StringBuilder insert(int offset, 任意类型) 
    将 boolean 参数的字符串表示形式插入此序列中。 
    
StringBuilder reverse() 
    将此字符序列用其反转形式取代。 
```

```java
public class Test{
    public static void main(String[] args){
        StringBuilder sb1 = new StringBuilder("1234abc");
	        
	     // 追加
	    StringBuilder sb2 = sb1.append("-def");
	    System.out.println(sb1); // 1234abc-def
	    System.out.println(sb2); // 1234abc-def
	    System.out.println(sb1 == sb2); // true
	        
	    // 插入
	    StringBuilder sb3 = sb1.insert(2, "java");
	    System.out.println(sb1); // 12java34abc-def
	    System.out.println(sb3); // 12java34abc-def
	        
	    // 反转内容
	    StringBuilder sb4 = sb1.reverse();
	    System.out.println(sb1); // fed-cba43avaj21
	    System.out.println(sb4); // fed-cba43avaj21
    }
}
```

## 3、ArrayList

Java集合类存放在java.util包中，集合其实就是一个大小可变的用来存放对象的容器

**注意点：**

1. **集合只能存放对象**。比如你存入一个int型数据66放入集合中，其实它是自动转换成Integer类后存入的，Java中每一种基本数据类型都有对应的引用类型。

2. **集合存放的都是对象的引用，而非对象本身**。所以我们称集合中的对象就是集合中对象的引用。对象本身还是放在堆内存中。

3. **集合可以存放不同类型，不限数量的数据类型**。

### 3.1 集合与数组的区别

数组：数组大小固定

集合：集合大小可以动态扩展

### 3.2 ArrayList概述

ArrayList类是在java.util中，该类需要导包

ArrayList底层是大小可变的数组的实现，存储在内的数据称为元素，也就是ArrayList可以不断地添加元素，其大小可以自动增长

```java
导包：
  Java.util.ArrayList<E>
    
<E>代表一种未知的数据类型，叫做泛型，用来约束集合中存储元素的数据类型
    
ArrayList<String> :表示该集合只能存储String型的对象
ArrayList<Student>:表示该集合只能用来存储Student型的对象
```

### 3.3 构造方法

```java
ArrayList()
    构造一个初始容量是10的空列表
```

```java
import java.util.ArrayList;

public class Test{
    public static void main(String[] args){
        // 创建一个ArrayList对象
        ArrayList<String> list = new ArrayList<String>();
        ArrayList<String> list2 = new ArrayList<>();
        
        // 不限制集合对象
        ArrayList list3 = new ArrayList();
    }
}
```

### 3.4 添加元素方法

```java
boolean add(E e) 
	将指定的元素追加到此列表的末尾。  
    
void add(int index, E element) 
	在此列表中的指定位置插入指定的元素。  
```

```java
import java.util.ArrayList;

public class Test{
    public static void main(String[] args){
        ArrayList<String> list = new ArrayList<String>();
        
        // 添加元素
        list.add("Hello");
        list.add("Hi");
        list.add("你好");
        System.out.println(list); // [Hello, Hi, 你好]
        
        // 任意位置插入
        list.add(1, "很好!"); // 不要超过最大索引
        System.out.println(list); // [Hello, 很好!, Hi, 你好]
    }
}
```

### 3.4 ArrayList常用方法

```java
boolean isEmpty()
	如果此列表不包含元素，则返回 true 。 
    
boolean remove(Object o) 
    删除指定的元素，返回是否删除成功
    
E remove(int index) 
    删除指定索引处的元素，返回被删除的元素  
    
int size()
    返回此列表中的元素个数
    
E set(int index, E element) 
    修改指定索引处的元素，返回被修改的元素
    
E get(int index) 
    返回指定索引处的元素
```

```java
import java.util.ArrayList;

public class Test{
    public static void main(String[] args){
        ArrayList<String> list = new ArrayList<String>();
        
        // 添加元素
        list.add("Hello");
        list.add("Hi");
        list.add("你好");
        list.add("Hi");
        System.out.println(list); // [Hello, Hi, 你好, Hi]
        
        // 任意位置插入
        list.add(1, "很好!");
        System.out.println(list); // [Hello, 很好!, Hi, 你好, Hi]
        
        
        // 删除元素
        // remove(Object o)
        list.remove("Hi");  // 如果有多个相同元素，remove会移除第一个出现的元素
        System.out.println(list); // [Hello, 很好!, 你好, Hi]
        
        // remove(int index)
        list.remove(1);
        System.out.println(list); // [Hello, 你好, Hi]
        
        // 返回元素的个数
        System.out.println(list.size()); // 3
        
        // 检查元素是否为空
        System.out.println(list.isEmpty()); // false
        
        
        // 修改列表元素
        list.set(1, "Hi");
        System.out.println(list); // [Hello, Hi, Hi]
        
        //查询指定索引处的元素
        System.out.println(list.get(1)); // Hi
    }
}
```

### 3.5 练习

#### 3.5.1 练习1

创建一个存储字符串的集合，存储3个字符串，在控制台遍历该集合

```java
import java.util.ArrayList;

public class Test1{
    public static void main(String[] args){
        // 创建ArrayList对象
        ArrayList<String> list = new ArrayList<String>();
        
        // 存储3个字符串
        list.add("今天");
        list.add("天气");
        list.add("很好");
        
        // 遍历列表
        for (int i = 0; i < list.size(); i++){
            System.out.println(list.get(i));
        }
    }
}
```

#### 3.5.2 练习2

创建一个存储学生对象的集合，存储3个学生，在控制台遍历输出

```java
// Student类
public class Student {
	private String name;
	private int age;
	
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
}
```

```java
// 测试类
import java.util.ArrayList;
import java.util.Scanner;

public class Test {
	public static void main(String[] args) {
		ArrayList<Student> list = new ArrayList<Student>();
		Scanner sc = new Scanner(System.in);
		
		// 存储学生
		addStudent(list, sc);
		addStudent(list, sc);
		addStudent(list, sc);
		
		// 遍历学生
		printAll(list);
	}
	
	
	// 遍历学生信息（集合）
	public static void printAll(ArrayList<Student> list) {
		for (int i = 0; i < list.size(); i++) {
			Student stu = list.get(i);
			System.out.println("姓名：" + stu.getName() + " 年龄：" + stu.getAge());
		}
	}
	
	
	// 添加学生信息（集合）
	public static void addStudent(ArrayList<Student> list, Scanner sc) {
		System.out.println("请输入学生姓名：");
		String name = sc.next();
		
		System.out.println("请输入学生年龄：");
		int age = sc.nextInt();
		
		Student student = new Student();
		student.setName(name);
		student.setAge(age);
		
		list.add(student);
	}
}
```

