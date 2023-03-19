<p align = "center" ><font size = 10， color = "# 009999">Array</font></p>

## Array

数组对任何一门语言来说都是重要的数据结构之一，不同的语言对数组的实现和处理方式也有所不同。

Java语言中提供的数组是用来==存储**固定大小**的同类型数据==。一般是存储在一块==连续的内存空间==中。

### 1、数组变量的定义格式

#### 1.1 数组变量的声明

首先必须先声明数组变量，才能在程序中使用，语法格式为

```java
数组的类型[] 数组名称;
dataType[] arrayRefVar; // 建议，首选
或
数组的类型 数组名称[];
dataType arrayRefVar[]; // 不建议，但没问题

例如：
    int[] array; // 首选
	int array[];
```

#### 1.2 创建数组

使用new创建数组，有三种方法定义数组

格式：==数组的类型[]  数组名称 = new  数组类型[数组的长度];==

```java
array = new dataType[arraySize];
上面创建数组做了两件事：
    1.使用dataType[arraySize]创建了一个数组
    2.将创建的数组的引用赋值给变量array

数组的声明和创建可以使用一条语句完成
数组的数据类型[] 数组名称 = new 数组数据类型[数组的长度];
第一种：
    dataType[] array = new dataType[arraySize];
	解释：
        1.左侧的数据类型规定了数组的数据类型
        2.[]表示数组的意思
        3.数组名称：给数组取一个名字
        4.=：表示赋值，把右边new出来的数组容器赋值给左边的数组变量，数组变量存储的是数组在内存空间中的地址值（十六进制）
        5.new:创建数组容器
        6.右侧数据类型应与左侧的数据类型保持一致
        7.arraysize顾名思义，就是给数组设置数组长度

第二种：
    dataType[] array = {value0, value1, ..., valuek};

第三种：
    dataType[] array = new int[]{value0, value1, value2, ..., valuek};
```

#### 1.3 注意事项

1. 数组属于引用数据类型，所以在**数组使用之前一定要开辟空间（实例化）**，如果使用了没有开辟空间的数组，则一定会出现 `NullPointerException` 异常信息
2. 数组的元素通过索引访问，**数组索引从0开始**，所以索引值从0到array.length - 1，访问数组时切记==不要超过数组的索引范围==

### 2、数组的使用

#### 2.1 数组的长度获取

在 Java 中提供有一种动态取得数组长度的方式：**数组名称.length**；

```java
int[] array = {1, 2, 3, 4, 5};
// 获取array的长度
System.out.println(array.length);
```

#### 2.2 数组的访问

数组访问是通过：**数组名[索引值]** 进行访问的

注意事项：

>1.使用[ ]按索引值获取数组元素，索引值**从0开始**
>
>2.使用[ ]可以读取数据，也可以修改数据
>
>3.索引值不能超过索引范围，否则会产生 java.lang.ArrayIndexOutOfBoundsException

```java
int[] array = {1, 2, 3, 4, 5};

// 通过数组名[index]访问数组
System.out.printlln(array[1]);
```

#### 2.3 数组的遍历

遍历就是将数组中的所有元素都访问一遍，一个不漏，一般通过for循环或for-each进行遍历

1. 方法一：for循环遍历

```java
int[] array = {1, 2, 3, 4, 5};
// 通过for循环遍历数组获取全部数据
for(int i = 0; i < array.length; i++){
    // 这里的i就是下标索引index
    System.out.println(array[i]);
}
```

2. 方法二：for-each

   for-each是for循环的另一种使用方式，能够更方便的完成对数据的遍历，可以避免循环条件和更新语句对错

   >格式：
   >
   >​	for(dataType  表达式1：表达式2){
   >
   >​			语句体3；
   >
   >​	}
   >
   >表达式1：数组当中每个元素类型的变量，一般是：dataType 数组变量名（自己取）
   >
   >表达式2：数组名

   >for-each原理
   >
   >遍历arrays中的每一个元素，把每一个元素取出来，然后赋值给array，最后打印每一个元素，知道arrays里面的元素全部都遍历完成

```java
int[] arrays = {1, 2, 3, 4, 5};
// 使用for-each形式遍历数组
for(int array : arrays){
    System.out.println(array);
}
```

3. for与for-each的区别

   >1：使用for循环可以拿到每一个元素以及元素的索引值，for-each则拿不到元素索引值，只能拿到元素。
   >
   >2：for循环因为有索引值，所以可以对数组元素进行修改和操作

### 3、Java中的内存分配

#### 3.1 运行时数据区域

Java 虚拟机在执行 Java 程序的过程中会把它管理的内存划分成若干个不同的数据区域。JDK 1.8 和之前的版本略有不同

JDK1.8之前：

![](images\Java1.8前运行时数据区.jpg)

JDK1.8之后：

![](images\JDK1.8之后的运行时数据区.jpg)

从图中可以看出：

**线程私有：**

- 程序计数器
- 本地方法栈
- 虚拟机栈

**线程共享：**

- 堆
- 方法区
- 直接内存（不在运行时数据区里）

Java 虚拟机规范对于运行时数据区域的规定是相当宽松的。以堆为例：堆可以是连续空间，也可以不连续。堆的大小可以固定，也可以在运行时按需扩展 。虚拟机实现者可以使用任何垃圾回收算法管理堆，甚至完全不进行垃圾收集也是可以的。

### 4、数组原理内存图

#### 4.1 一个数组的内存图

##### 4.1.1 内存

```java
1.方法区：存储可运行的.class文件
2.栈：方法运行时使用的内存，比如main运行，进入栈中运行
3.堆内存：存储对象或者数组，new来创建的，都存储在堆内存
4.寄存器：给cup使用：无关
5.本地方法栈：JVM使用操作系统功能的时候 ：无关
```

>**栈内存**：用于存储局部变量表，当数据使用完，所占空间**自动释放**
>
>**堆内存**：
>
>1. 数组和对象，==所有用new建立的实例都存放在堆中==
>2. 每个实例都有内存地址值
>3. 实体中的变量都有默认初始值
>4. 实体不被使用之后会在不确定的时间内被==垃圾回收器回收==

##### 4.1.2 数组数据初始默认值

```java
1.整型初始默认值：0
2.浮点型初始默认值：0.0
3.字符型char默认初始值：空白字符
4.引用数据类型默认初始值：null
5.boolean型默认初始值：false
```

##### 4.1.3 内存图解

```java
public static void main(String[] args){
    int[] arr = new int[3]; // 动态初始化
    System.out.println(arr);// 地址值
    System.out.println(arr[0]);
    System.out.println(arr[1]);
    System.out.println(arr[2]);
    
    // 此处修改arr的值
    arr[0] = 10;
    arr[1] = 20;
    System.out.println(arr); // 地址值
    System.out.println(arr[0]); // 10
    System.out.println(arr[1]);  // 20
    System.out.println(arr[2]); // 0
}

运行此代码得到的结果为：
[I@1....
0
0
0
[I@1....
10
20
0
```

![](images\一个数组的内存图.png)

#### 4.2 两个数组的内存图

```java
public static void main(String[] args){
    int[] arr = new int[3]; // 动态初始化
    System.out.println(arr);// 地址值
    System.out.println(arr[0]);
    System.out.println(arr[1]);
    System.out.println(arr[2]);
    
    // 此处修改arr的值
    arr[0] = 10;
    arr[1] = 20;
    System.out.println(arr); // 地址值
    System.out.println(arr[0]); // 10
    System.out.println(arr[1]);  // 20
    System.out.println(arr[2]); // 0
    
    
    int[] arr1 = new int[3]; // 动态初始化
    System.out.println(arr1);// 地址值
    System.out.println(arr1[0]);
    System.out.println(arr1[1]);
    System.out.println(arr1[2]);
    
    // 此处修改arr的值
    arr1[0] = 11;
    arr1[1] = 22;
    System.out.println(arr1); // 地址值
    System.out.println(arr1[0]); // 11
    System.out.println(arr1[1]);  // 22
    System.out.println(arr1[2]); // 0
    
}
```

![](images\两个数组的内存图.png)

#### 4.3 两个变量一个数组的内存图

```java
public static void main(String[] args){
    int[] arr = new int[3]; // 动态初始化
    System.out.println(arr);// 地址值
    System.out.println(arr[0]);
    System.out.println(arr[1]);
    System.out.println(arr[2]);
    
    // 此处修改arr的值
    arr[0] = 10;
    arr[1] = 20;
    System.out.println(arr); // 地址值
    System.out.println(arr[0]); // 10
    System.out.println(arr[1]);  // 20
    System.out.println(arr[2]); // 0
    
    
    int[] arr1 = arr; 
    
    System.out.println(arr1);// 地址值
    System.out.println(arr1[0]);
    System.out.println(arr1[1]);
    System.out.println(arr1[2]);
    
    // 此处修改arr的值
    arr1[0] = 11;
    arr1[1] = 22;
    System.out.println(arr1); // 地址值
    System.out.println(arr1[0]); // 11
    System.out.println(arr1[1]);  // 22
    System.out.println(arr1[2]); // 0
    
}
```

![](images\两个变量一个数组内存图.png)

### 5、数组索引越界异常

**问题**：首先创建一个长度为3数组，此数组的索引值范围为0-2，当访问超过2的数组下标时，会出现数组索引越界异常。

**解决方法**：查看异常信息，根据情况去代码中找到异常位置进行修改

```java
public static void main(String[] args){
    int[] arr = new arr[3];
    // 访问索引3，arr中不存在，越界了
    System.out.println(arr[3]);
}
结果：抛出"数组索引出界异常"
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 3  
```

### 6、数组空指针异常

**问题**：所有的引用类型变量都可以赋值为null值，数组就是一个引用类型变量，数组必须进行new初始化才能够使用其中的元素。如果只是进行了一个null，没有进行new创建，那么将会发生空指针异常–NullPointerException

>1.NullPointerException是由RuntimeException派生出来，是一个**运行级别**的异常。意思是说可能会在运行的时候才会被抛出，而且需要看这样的运行级别异常是否会导致你的业务逻辑中断。
>
>2.==空指针异常==，就是一个指针是空指针，你还要去操作它，既然它指向的是空对象，它就不能使用这个对象的方法。

``` java
public static void mian(String[] args){
    int[] arr = null;
    System.out.println(arr) // null
    System.out.println(arr[0]);
}

结果：抛出"空指针异常"
Exception in thread "main" java.lang.NullPointerException
```

### 7、Arrays类

>Arrays类中包含用于操作数组的各种方法（例如排序和搜索）。 此类还包含一个静态工厂，允许将数组视为列表，它提供的所有方法都是静态的。
>
>**导入**：import java.util.Arrays;
>
>**调用**：Arrays.方法（）进行调用



>1.替换元素以及填充元素：通过 fill 方法。
>2.对数组排序：通过 sort 方法,按升序。
>3.比较数组：通过 equals 方法比较数组中元素值是否相等。
>4.查找数组元素：通过 binarySearch 方法能对排序好的数组进行二分查找法操作。

#### 7.1 Arrays.fill()

两种用途：

1. 填充数组，将数组中的全部元素转换为所输入的元素
2. 替换数组元素，将数组中的某些元素进行替换

第一类：填充数组

```java
import java.util.Arrays; // 导包

public class Fill{
    public static void main(String[] args){
        int[] arrs = new int[3];
        arrs[0] = 3;
        System.out.println("原始数据为:");
        for(int arr: arrs){
            System.out.println(arr);
        }
        System.out.println();
        Arrays.fill(arrs, 4); // 为数组填充4
        System.out.println("填充后的数据为：");
        for(int arr: arrs){
            System.out.println(arr); // 遍历数组
        }
    }
}

结果为：
原始数据为:
3 0 0 
填充后的数据为：
4 4 4 
```

第二种：替换数组元素

>**格式**：Arrays.fill(列表名称, 起始索引(fromIndex), 终止索引(toIndex), 改变的数值(val)）
>
>不包括终止的索引，终止在终止索引前一位

```java
// 在上述代码基础上修改
// 这是一个特殊的格式Arrays.fill(列表名称, 起始索引(fromIndex), 终止索引(toIndex), 改变的数值(val)）
Arrays.fill(arrs, 2, 4, 4); // 填充数组
```

#### 7.2 Arrays.sort(int[] a)（重要，常用）

在代码编译过程中，有时候会需要用到有序的一组数组才能进行更好的操作, Java中提供了sort方法对数组的元素进行**升序排序！**

```java
import java.util.Arrays;
public class Sort{
    public static void main(String[] args){
        int[] mylist = {1,7,33,4};
        Arrays.sort(mylist);
        //方式为Arrays.sort(列表)
        for(int x:mylist){
            System.out.println(x);
        }
    }
}
```

#### 7.3 Arrays.equals(int[] a, int[] a2)

**比较两个数组是否相同**

问题：Arrays.equals(...)与Object中的equals方法有什么不同？

```java
import java.util.Arrays;

public class Equals{
    public static void main(String[] args){
        int[] arr1 = {1, 2, 3, 4};
        int[] arr2 = {1, 2, 3, 4};
        System.out.println(Arrays.equals(arr1, arr2)); // true
        System.out.println(arr1.equals(arr2));//false
    }
}
```

#### 7.4 Arrays.copyOf()（不常用）

**Arrays.copyOf(int[] original, int newLength)复制指定的数组---效率低，会重新开辟新的数组空间**

original - 要复制的数组;

newLength - 要返回的副本的长度

```java
import java.util.Arrays;
public class Test {
    public static void main(String args[]) {
        int [] arrA={23,34,345,234};
        int [] arrB=new int[5];// 默认值0
        System.out.println("拷贝前："+ arrB);
        arrB=Arrays.copyOf(arrA, 5);  //重新开辟空间
        System.out.println("拷贝后："+ arrB);
        System.out.println(Arrays.toString(arrB));
    }
}

结果：
拷贝前：[I@1....
拷贝后：[I@4....
[23, 34, 345, 234, 0]
```

#### 7.5 Arrays.binarySearch(int[] a, int key)

1. 使用二分法查找，必须先对数组进行排序;

2. 用二分查找算法在给定数组中搜索给定值的对象(Byte,Int,double等)。数组在调用前必须排序好的。如果查找值包含在数组中，则返回搜索键的索引；否则返回 (-(*插入点*) - 1)。

```java
import java.util.Arrays;
public class Test {
    public static void main(String[] args) {
        int[] a = {1, 2, 323, 23, 543, 12, 59};
        System.out.println(Arrays.toString(a));
        Arrays.sort(a);   //使用二分法查找，必须先对数组进行排序;
        System.out.println(Arrays.toString(a));
        //返回排序后新的索引位置,若未找到返回负数。
        System.out.println("该元素的索引："+ Arrays.binarySearch(a, 12)); 
    }
}
```

#### 7.6 Arrays.toString() 打印数组

此处的Arrays.toString()方法是Arrays类的静态方法，不是Object的toString()方法。

```java
import java.util.Arrays;
public class Test {
    public static void main(String args[]) {
        int[] a = {1, 2};
        System.out.println(a); // 打印数组引用的值；地址
        System.out.println(Arrays.toString(a)); // 打印数组元素的值；
    }
}
```

## 8、二维数组(理解即可)

#### 8.1 概述

二维数组也是一种容器，不同与一维数组，该容器中存储的是一维数组

#### 8.2 二维数组初始化

```java
格式：
    数据类型[][] 数组变量名 = new 数据类型[m][n];
	m:表示行，也可以认为是可以存放多少个一维数组
    n:表示列，也可以认为是每个一维数组中有多少个元素
    比如：
        int[][] arr = new int[2][3];
		表示该数组可以存放2个一维数组，每个一维数组可以存放3个元素
        
三种初始化方式：
    type[][] array = new type[2][3]; // 给定空间再赋值
	type[][] array = new type[][]{value1,..., valuek}; // 在定义时初始化
	type[][] array = new type[size1][]; // 数组第二维长度为空，可变化
```

#### 8.3 二维数组访问

```java
访问二维数组：
	格式：数组名[索引1][索引2]
	索引1：二维数组中一维数组的索引
	所引2：一维数组中元素的索引
```

#### 8.4 二维数组求和

二维数组的求和是利用双层循环方式实现的

```java
public class Test{
    public static void main(String[] args){
        // 定义二维数组
        int[] arr = {{1, 2, 3}, {2, 3, 4}};
        int sum = 0;
        for (int i = 0; i < arr.length; i++){
            for (int j = 0; j < arr[i].length; j++){
                sum += arr[i][j];
            }
        }
        System.out.println("二维数组的和为：" + sum);
    }  
}
```

