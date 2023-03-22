## 数据结构类型互换

### 1、将数字转化为String

在Java中，可以使用**String.valueOf()**将包装型以及基本数据类转化为String。

#### 1) String.valueOf()

String.valueOf()是最常用的方法，对于包装类以及基本数据类型都适用。

```java
// String.valueOf()对int和Integer都适用
Integer num = 10123;
// int num = 100123;
// 利用String.valueOf()将Integer/int型转化为String
String s = String.valueOf(num);
System.out.println(s);
```

#### 2) toString()

toString()只适用于包装类，基本数据类型需要先调用具体包装类的 ValueOf() 方法再使用。

```java
Integer num = 10123;
// 利用toString()将Integer型转化为String
String s = num.toString();
System.out.println(s);
```

#### 3) Integer.toString()

Xxx.toString()适用于基本数据类型

```java
int num = 10123;
// 利用Integer.toString()将int型转化为String
String s = Integer.toString(num);
System.out.println(s);
```

#### 4）直接拼接空字符串

```java
int num = 10123;
String s = num + "";
System.out.println(s);
```

### 2、将String转化为数字

#### 1) 使用包装类的valueOf()方法

通过包装类的valueOf()方法，可以将字符串转化为想要的==包装类==，如Byte，Short，Integer，Long，Float，Double都有对应的valueOf()方法

```java
String test = "12345";
Integer int1 = Integer.valueOf(test);
Double double1 = Double.valueOf(test);
```

#### 2) 使用包装类的parseXXX()方法

通过包装类的parseXXX()方法，可以将字符串转化为想要的基本数据类型，同上都有相应的parseXXX()方法

```java
String test = "1235";
int int2 = Integer.parseInt(test);
double double2 = Double.parseDouble(test);
```



### 3、将int型整数转化为int型数组

#### 1) 方法一（通用）不知道数字位数

1. 先将int型数字转化为字符串，使用String.valueOf(int s)或者Integer.toString()
2. 新建一个int型数组来保存数字的每一位，int[] arr = new int[这里一定要填长度];
3. 利用for遍历字符串将每一位数字添加到数组中，先取出字符串的每一位存入Character型，再将Character转化为String，再将String转化为int型再存进int型数组中。

```java
public class Exchange {
    public static void main(String[] args) {
        int num = 10123;
        // 利用String.valueOf()将int型转化为String
        String numStr = String.valueOf(num);
        // 新建一个数组用于保存数字的每一位
        int[] array = new int[numStr.length()];
        // 遍历字符串将每一位添加到数组中
        for (int i = 0; i < numStr.length(); i++) {
            // 将字符串中的每一位存入ch中，charAt(int index)返回指定索引处的char值。
            Character ch = numStr.charAt(i);
            // Integer.parseInt(String s)调用了Integer.parseInt(String s, int radix)函数来处理String到int的转换
            array[i] = Integer.parseInt(ch.toString());
        }
        // 遍历数组，查看情况
        for (int arr:array){
            System.out.println(arr);
        }
    }
}
```

#### 2) 方法二（知道数字位数）

不需要转化为String型，直接存进数组中

==注意==：这种方法得到的数组中的数字顺序和原始数据的顺序相反

```java
public class Exchange {
    public static void main(String[] args) {
        int num = 10123;
        // 新建一个数组用于保存数字的每一位
        int[] array = new int[5];
        // 遍历字符串将每一位添加到数组中
        for (int i = 0; i < 5; i++) {
            array[i] = num % 10;
            num / 10;
        }
        // 遍历数组，查看情况
        for (int arr:array){
            System.out.println(arr);
        }
    }
}
```

### 4、将int型数组转化为数字

方法：直接利用数字的特性将数组中的每个数字取出进行处理

```java
int arr[] = {1,4,8,7,8};
int num = 0;
for(int i = 0; i  < arr.length; i++){
	num = num * 10 + arr[i];
}
```

### 5、字符串转化为数组

#### 1）toCharArray()

Java String 类中的toCharArray()方法将字符串转化为字符（char）数组

```java
String s = "123adf";
char[] arr = s.toCharArray(); // char数组
// 遍历arr
for(int i = 0; i < arr.length; i++){
    System.out.println(arr[i]);
}
```

#### 2）String.spilt()

Java通常用split()分割字符串，返回的是一个String字符串数组

```java
String s = "addf134";
String[] arr = s.split("");
for(int i = 0; i < arr.length; i++){
    System.out.println(arr[i]);
}
```

#### 3）getBytes()（不常用）

要返回 byte 数组就直接使用 getBytes 方法

```java
String s = "123abc" ;
byte [] arr = s.getBytes();
```

### 6、数组转化为字符串

#### 1）String.copyValueOf(charArray)

char 字符数组转化为字符串，使用 String.copyValueOf(charArray) 函数实现

```java
char[] arr = { 'a', 'b', 'c' };
String string = String.copyValueOf(arr);
System.out.println(string); // 输出abc
```

#### 2）String字符串数组转化为字符串

```java
String[] arr = { "123", "abc" };
StringBuffer sb = new StringBuffer();
for (int i = 0; i < arr.length; i++) {
    sb.append(arr[i]); // String并不拥有append方法，所以借助 StringBuffer
}
String sb1 = sb.toString();
System.out.println(sb1); // 输出123abc
```
