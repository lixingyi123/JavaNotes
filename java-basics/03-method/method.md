<p align = "center" ><font size = 10， color = "#009999">Method</font></p>

### 1、方法的概念和格式

#### 1.1 方法的概念

>1、public static void main(String[] args){}中
>
>1. main（）方法是主方法，由==JVM调用==，程序的入口
>
>2. **public static** ：是修饰符，固定写法
>
>3. main:方法名
>
>4. String[] args:是形式参数
>
>   
>
>2、System.out.println();中：
>
>1. println()是一个输出方法
>2. out是标准输出对象
>3. System是一个系统类

方法：就是将具有独立功能的代码组织成为一个整体，使其具有特殊功能的代码块。将具有特殊功能的一段代码，使用**大括号{}括起来**，添加必要的修饰符，方便使用。
    1.方法是解决一类问题的步骤的有序组合
    2.方法包含在**类与对象**中
    3.方法在程序中被创建，在**其他地方被使用**

#### 1.2 方法的定义

```java
方法格式语法：
    修饰符 返回值类型 方法名称(参数列表){
    	...
        方法体(功能代码);
        ...
        return 返回值; // 按照需求判断,结束方法返回方法的调用处，如果返回值类型维void,省略不写
}

格式解释：
    1.修饰符：可选非必须，告诉编译器如何调用该方法，定义了该方法的访问类型，目前是固定写法：public static
    2.返回值类型：方法必须有返回值类型，有返回值时，returnValueType是方法返回值的数据类型。没有返回值时returnValueType是void型
    3.方法名：给方法取一个名字，取方法名尽量要见名知意，使用小驼峰命名法
    4.参数列表：参数相当于占位符（被称作形参），没有参数时也必须有小括号。当方法被调用时，传值给参数，这个值被称为实参或变量。可选
    5.方法体（功能代码）：方法体中包含具体的语句，定义该方法的功能
    6.return：结束方法，返回方法的调用处
```

![](images\方法定义格式.png)

#### 1.3 方法三要素

1. 方法名称：见名知意，小驼峰
2. 参数列表
3. 返回值类型

#### 1.4 方法的作用

1. 解决代码冗余，简化程序
2. 方便修改，方便锁定问题，方便管理

#### 1.5 方法的注意事项

```java
注意事项：
    1.方法不能嵌套定义，但可以调用其他方法
    2.如果方法的返回值类型不是void，那么方法体中必须有与声明类型相同的return语句
    3.方法执行结束后没有任何返回值，那么返回值类型必须写成void
    4.return语句一旦执行，就表示该方法已经结束，所以return后面的语句将不再执行，属于无效代码
    5.方法的形参可以是0个，1个或者多个，是多个的时候要用逗号隔开，传入的时候也是用逗号隔开
    6.方法的形式参数列表中起决定性作用的是参数的类型，而不是变量名
    7.所有带有static关键字的方法被调用时，都采用类名称.方法名(实际参数列标配)
```

### 2、无返回值无参数方法的定义和调用（打印语句）

#### 2.1 定义

![](images\无返回值无形参方法定义.png)

>注意点：
>
>​	1.方法体放在大括号里
>
>​	2.方法名采用小驼峰形式命名

#### 2.2 调用

注意：

1. 方法定义完毕后，不调用不执行
2. 调用方法：方法名称(...)；
3. 方法可以调用很多次，只有调用才会执行

```java
// 同class中的调用
// 方法名(..);调用一次执行一次，方法可以调用任意次
class TestDiver{
    public static void main(String[] args){
        System.out.println("游戏开始！");
        System.out.println("看到第一个敌人！！！");
        fire(); // 直接调用方法
        System.out.println("开第五枪！！，第一个敌人倒下");
        
        System.out.println("看到第二个敌人！！！");
        fire(); // 直接调用方法
        System.out.println("开第五枪！！，第二个敌人倒下");
        
        System.out.println("看到第三个敌人！！！");
        fire(); // 调用方法
        System.out.println("开第五枪！！，第三个敌人倒下");
    }
    
    public static void fire(){
        System.out.println("开第一枪！！");
        System.out.println("开第二枪！！");
        System.out.println("开第三枪！！");
        System.out.println("开第四枪！！");
    }
}
```

```java
// 调用2
class Dog{
    int size;
    int name;
    
    void bark(){
        if(size > 60){
            System.out.println("Wooof!");
        }else if(size > 14){
            System.out.println("Ruff!");
        }else{
            System.out.println("Yip!")
        }
    }
}


class DogTestDiver{
    public static void main(String[] args){
        Dog dog = new Dog(); // 创建对象
        dog.size(70);
   
        dog.bark();
    }
}
```

```java
调用2步骤：
   1.定义方法
   2.创建类的对象，形如：Dog dog = new Dog();
   3.通过对象名.方法名()的形式调用方法，例如：dog.bark();
```

```java
// 练习需求：定义一个方法，打印输出方法内部的数据（方法内部的变量）是否是偶数？

public class Test{
    public static void main(String[] args){
        iseven();
    }
    
    public static void iseven(){
        int num = 10;
        boolean even = num % 2 == 0?true:false;
        System.out.println(num + "是否是偶数" + even);
    }

}
```

### 3、带参数无返回值方法调用图（简单功能）

![](images\无返回值带参数方法.png)

```java
// 简单使用
// 需求：定义一个方法，用于打印两个int中数字的最大值，数据来自于方法参数

public class PrintMax{
    // 打印两数之间的最大值
    public static void main(String[] args){
    	printMax(36, 23);
    }


	public static void printMax(int a, int b){
    	int max = (a > b) ? a : b;
    	System.out.println("最大值为" + max);
	}
}

```

### 4、带参数带返回值的方法调用（拿到方法数据）

**返回值：完成一个方法之后，需要得到方法执行之后得到的数据，并返还给方法的调用者**

![](images\无参有返回值方法.png)

```java
当方法返回一个值的时候，方法调用通常被当做一个值。例如：
int larger = max(30, 40);

// 练习：也是求两数的最大值，但是需要从方法处返回最大值
public class GetMax {
   /* 主方法 */
   public static void main(String[] args) {
      int a = 5, b = 2;
      int max = getMax(a, b);
      System.out.println( a + " 和 " + b + " 中，最大值是：" + max);
   }
 
   /* 返回两个整数变量较大的值 */
   public static int getMax(int num1, int num2) {
      int max = (x >= y) ? x : y;
	  return max; // 结束方法，并且把max中的数据，返还给方法的调用者
   }
}
```



### 5、形式参数和实际参数的区别

>形参：顾名思义:就是**形式参数**，用于定义方法时定义的参数，是用来接收调用者传递的参数的。
>		   **形参只有在方法被调用的时候，虚拟机才会分配内存单元，在方法调用结束之后便会释放所分配的内存单元。**
>	       因此,==形参只在方法内部有效==，所以针对引用对象的改动也无法影响到方法外
>
>​		   定义形式参数的时候是没有值的，当调用方法时才会有值
>
>实参：顾名思义:就是**实际参数**，用于调用时传递给方法的参数。实参在传递给别的方法之前是要被预先创建并赋值的。

注意点：
在==值传递==调用过程中，只能把实参传递给形参，而不能把形参的值反向作用到实参上（拷贝传递）。在函数调用过程中，形参的值发生改变，而实参的值不会发生改变。
而在==引用传递==调用的机制中，实际上是将实参引用的地址传递给了形参，所以任何发生在形参上的改变也会发生在实参变量上。

### 6、方法的重载

#### 6.1 认识

1. 概念：在同一个类中，多个功能相同，但是参数列表不同的多个方法，可以使用相同的方法名称，这种**同名不同参**的方法，可以存在同一个类中，这叫做方法的重载
2. 作用：
   - 减少程序的学习和使用成本
   - 减少方法名称的数量

3. 调用:
   - 根据名称找到对应的方法
   - 根据参数的数量找到对应的方法
   - 根据参数类型确定最终要调用的方法（类型匹配，类型顺序匹配）

```java
//1.定义一个方法，获取两个int类型的数字和
//2.定义一个方法，获取三个int类型的数字和
//3.定义一个方法，获取两个double类型的数字和
//4.定义一个方法，获取三个double类型的数字和

public static void main(String[] args){
    System.out.println(getSum(10, 20));
    System.out.println(getSum(10, 20, 30));
    System.out.println(getSum(10.0, 20.0));
    System.out.println(getSum(10.0, 20.0, 30.0));
}

public static int getSum(int a, int b){
    return a + b;
}

public static int getSum(int a, int b, int c){
    return a + b + c;
}

public static double getSum(double a, double b){
    return a + b;
}

public static double getSum(double a, double b, double c){
    return a + b + c;
}
```

#### 6.2 注意事项

同名，同类，不同参

>方法重载与哪些因素有关
>
>1.参数的数量
>
>2.参数类型
>
>3.多个参数，参数的顺序

```java
// 练习：使用方法重载的思想，比较两数是否相同兼容全整型
public static void main(String[] args){
    System.out.println(compare((byte)10, (byte)20));
    System.out.println(compare((short)10, (short)20));
    System.out.println(compare(10, 20));
    System.out.println(compare(10L, 20L));
}

public static boolean compare(byte a, byte b){
    System.out.println("Byte");
    boolean result = (a == b) ? true : false;
    return result;
}

public static boolean compare(short a, short b){
    System.out.println("Short");
    return a == b;
}

public static boolean compare(int a, int b){
    System.out.println("Int");
    boolean result;
    if(a == b){
        result = true;
	}else{
        result = false;
    }
    return result;
}

public static boolean compare(long a, long b){
    System.out.println("Long");
    if (a == b){
        return true;
    }else{
        return false;
	}
}
```

### 7、方法参数的传递

参数传递：可以理解为当我们要调用一个方法时，我们会把指定的数值，传值给方法中的参数（定义方法时中定义的变量），这样方法中的参数就有了指定的值，可以使用该值。这种传递方式，我们称为参数的传递

#### 7.1 基本数据类型的参数传递

注意：

1. 基本类型变量，保存的是具体的值
2. 基本数据类型作为形式参数，形式参数的改变，不会影响实际参数的（拷贝传递）

```java
public class DemoBaseVar {
	public static void main(String[] args) {
		
		int a = 10;
		System.out.println("调用方法前a的值：" + a);// 10
		//调用方法
		change(a);
		System.out.println("调用方法后a的值：" + a);// 10		
	}

	public static void change(int a) {//int a = 10 ;int b = 20
		// int a = 10
		System.out.println("调用时的a值：" + a);// 10
		a = a*10;
		System.out.println("调用时a改变后的值：" + a);// 100
		
	}
	
}

```

![](D:\javalearn\java资料\Java\method-prepare\images\方法基本数据类的值传递.png)

#### 7.2 引用数据类型的参数传递

注意：

1. 引用数据变量保存的是堆内存空间的地址值，进行参数传递时传递也是地址值
2. 引用数据类型作为形式参数，形式参数的改变，会影响实际参数

```java
public class DemoBaseVar {
	public static void main(String[] args) {
		
		int[] arr = {10, 20};
        System.out.println(arr);// arr的地址值
		System.out.println("调用方法前arr[0]的值：" + arr[0]);// 10
        System.out.println("调用方法前arr[1]的值：" + arr[1]);// 20
		//调用方法
		change(arr);
		System.out.println("调用方法后arr[0]的值：" + arr[0]);// 100
        System.out.println("调用方法后arr[1]的值：" + arr[1]);// 200
	}

	public static void change(int[] arr) {
		
		System.out.println("调用时的arr[0]的值：" + arr[0]);// 10
        System.out.println("调用时的arr[1]的值：" + arr[1]);
		arr[0] = 100;
        arr[1] = 200;
		System.out.println("调用时arr[0]改变后的值：" + arr[0]);// 100
		System.out.println("调用时arr[1]改变后的知：" + arr[1]);
	}
}
```

![](images\方法引用类型参数传递.png)

练习：需求1：定义一个方法，用于数组的遍历（打印数组元素）

要求遍历结果在一行上：**[11, 22, 33, 44, 55]**

原数组：{11, 22, 33, 44, 55}

```java
public static void main(String[] args){
    int[] array = {11, 22, 33, 44, 55};
    printArr(array);
}
public static void printArr(int[] arr){
    System.out.print("[");
    for(int i = 0; i < arr.length; i++){
        if(i == arr.length - 1){
            System.out.print(arr[i] + "]");
        }else{ 
            System.out.print(arr[i] + ",");
        }
    } 
}
```

练习2：设计一个方法，用于获取数组元素的最大值

```java
public static void main(String[] args){
    
    int[] array = {11, 655, 23, 5667,212};
    int max = getMax(array);
    System.out.println("最大值为：" + max);
 
}


public static int getMax(int[] arr){
    
    int max = arr[0];
    
    for(int i = 1; i < arr.length; i++){
        
        if(max < arr[i]){
            max = arr[i];
        }
    }
    
    return max;
}
```

