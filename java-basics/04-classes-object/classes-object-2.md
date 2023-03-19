<p align = "center" ><font size = 10， color = "# 009999">Classes & Objects</font></p>

## 1、匿名对象

**匿名对象就是没有名字的对象**

```java
1. 有名字的对象：
    Student stu = new Student();
2. 匿名对象：
    new Student();
3. 匿名对象特点：只能使用一次
```

```java
// Student类
public class Student {
	// 成员变量
	private int id;;
	private String name;
	
    // 无参构造方法
	public Student() {
		super();
	}
		
	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
	
    // 方法
	public void show(int age, String name) {
		System.out.println(age + "," + name);
	}	
}
```

```java
// 测试类
public class StudentTestDrive {
	public static void main(String[] args) {
		// 有名字的对象
		Student student = new Student();		
		student.show(18, "xxx");
        
		// 匿名对象
		new Student().show(18, "xxx");
	}
}
```

## 2、继承

​	继承：在Java中指的是一个类可以继承另一个类，被继承的类叫做父类/超类/基类，继承它的类叫做子类，继承后**子类中就拥有了父类中的所有成员**==（成员变量和方法）==，子类就不需要重新定义了

### 2.1 继承的好处

```java
1.提高了代码的复用性
2.使类与类之间产生了关系
```

例子：练习

```java
// Person类
public class Person {
	String name;
	int age;
	
	// 功能方法
	public void eat() {
		System.out.println("吃");
	}
	
	public void sleep() {
		System.out.println("睡");
	}
}
```

```java
// Teacher类继承Person类
public class Teacher extends Person{
	// 独有的属性
	double salary;
	
	// 独有的方法
	public void teach() {
		System.out.println("教学生"); 
	}
}
```

```java
// 测试类
public class Test {
	public static void main(String[] args) {
		Teacher teacher = new Teacher();
		
		System.out.println(teacher.age);
		System.out.println(teacher.salary);
		
		teacher.teach();
        
		teacher.sleep();
		teacher.eat();
	}

}
```

### 2.2 继承的格式

在Java中**通过extends关键字**可以申明一个类是从另外一个类继承而来的

**优点**：**通过继承可以将一些共性属性，行为抽取到一个父类，子类只需要继承**就可以了，由此提高代码的复用性，但同时也提高了类与类之间的耦合性（缺点）

```java
格式：
    public class 父类类名{
        ...
    }

	public class 子类类名 extends 父类类名{
        ...
    }
```

### 2.3 继承后成员访问规则

1. 继承后构造方法的访问规则：**父类的构造方法不能被子类继承**

```java
class Father{
	public Father() {
		System.out.println("Father 无参构造方法");
	}
	public Father(int age, String name) {
		System.out.println("Father 有参构造方法");
	}
}

class Son extends Father{

}


public class Test1 {
	public static void main(String[] args) {
		Son son = new Son(18, "xxx"); // 报错，说明子类不可以继承父类的构造方法
		
	}
}
```

2. 继承后私有成员的访问规则：

   **父类的私有成员(私有成员变量以及私有成员方法)可以被子类继承，但子类不能直接访问**

```java
class Father{
	private int age = 20;
	
	private void method() {
		System.out.println("私有方法");
	}
}

class Son extends Father{

}

public class Test1 {
	public static void main(String[] args) {
		Son son = new Son();
		System.out.println(son.age); // 编译报错
		son.method(); // 报错,来自类型Father的方法method()是不可见的
		
	}
}
```

3. 继承后非私有成员的访问规则

   ​	**当通过子类访问非私有成员，先在子类中找，如果找到就使用子类的，找不到就去父类中找**

```java
class Father{
	int age = 20;
	String name = "xxx";
	
	public void method() {
		System.out.println("Father中的非私有方法");
	}
}

class Son extends Father{
	int age = 48;
	public void method() {
		System.out.println("Son中的非私有方法");
	}

}

public class Test1 {
	public static void main(String[] args) {
		Son son = new Son();
		System.out.println(son.age);// 48
		System.out.println(son.name); // xxx
		son.method(); // Son中的非私有方法
		
	}
}
```

### 2.4 方法重写

**方法重写：**子类中出现与父类一模一样的方法（**返回值类型，方法名和参数列表 都相同**），会出现覆盖的效果，称为重写或者复写。**声明不变，重新实现**

```java
// 父类
class Father{
    
	public void method() {
		System.out.println("Father method");
	}
}

// 子类
class Son extends Father{
	
	@Override // 代表下面这个方法是重写
	public void method() {
		System.out.println("Son method");
	}
	
	public void show() {
		System.out.println("show");
	}
}

// 测试类
public class Test1 {
	public static void main(String[] args) {
		Son son = new Son();
		son.method(); // Son method
	}
}
```

#### 2.4.1 方法重写的注意事项

1. **一定是父子关系**

2. 子类中重写的方法==返回值类型，方法名，参数列表==一定要和父类一模一样

3. 子类重写的方法可以使用**@Override注解**进行标识，如果不是重写的方法，使用@Override注解就会报错

   **这里建议开发中只要是重写方法就加上@Override注解**

4. 子类重写父类的方法时，不能低于父类的访问权限

   访问权限：public-->protected-->默认（不写）-->private

### 2.5 super与this关键字

```java
this：代表当前对象本身
    this可以访问：本类的成员属性，成员方法，构造方法

super：调用父类
    super可以访问：父类的成员属性，成员方法，构造方法
```

#### 2.5.1 super

#####  2.5.1.1 super的使用

```java
class Father1{
	protected void sport() {
		System.out.println("Father 跑4圈");
	}
	
	public void run() {
		System.out.println("Father 第一圈");
		System.out.println("Father 第二圈");
		System.out.println("Father 第三圈");
	}
}

class Son1 extends Father1{
	
	@Override
	// 使用super
	public void sport() {
		// TODO Auto-generated method stub
        System.out.println("有super");
		super.sport(); 
		System.out.println("Son 游泳");
		System.out.println("=============");
	}
	
	@Override
	public void run() {
		// 不使用super
		System.out.println("没有super");
		System.out.println("Son 第一圈");
		System.out.println("Son 第二圈");
		System.out.println("Son 第三圈");
	}
}
public class Test3 {
	public static void main(String[] args) {
		Son1 son1 = new Son1();
		son1.sport();
		son1.run();		
	}
}

// 结果
有super
Father 跑4圈
Son 游泳
=============
没有super
Son 第一圈
Son 第二圈
Son 第三圈
```

##### 2.5.1.2 super关键字的用法

1. **访问父类的成员方法**：super.成员变量名；

```java
class Father{
    int num = 10;
}

class Son extends Father{
    int num = 20;
    public void show(){
        System.out.println("父类的成员变量：" + super.num);
        System.out.println("本类的成员变量：" + num);
    }
}

public class Test{
    public static void main(String[] args){
        Son son = new Son();
        son.show();
    }
}
```

2. **访问父类的成员方法**：super.成员方法；

```java
class Father{
	int num = 20;
	public void method() {
		System.out.println("父类成员方法");
	}
}

class Son extends Father{
	int num = 48;
	public void show() {
		super.method();
	}

}


public class Test1 {
	public static void main(String[] args) {
		Son son = new Son();
		son.show();
	}
}
```

3. **访问父类的构造方法**	

- **子类的构造方法会默认调用父类的空参构造**
- **如果父类中没有空参构造方法，只定义了子类有参构造方法，会编译报错**
- super访问父类的构造方法可以用来初始化从父类继承过来的属性
- 在子类的构造方法中，使用super调用父类的构造方法，必须放在子类构造方法的第一行

```java
class Father{
	private int age;
	private String name;
	
    // 无参构造方法
	public Father() {

	}
	
    // 有参构造方法
	public Father(int age, String name) {
		this.age = age;
		this.name = name;
	}
	
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	
}


class Son extends Father{
	// 子类这里不写成员变量
	public Son() {
		
	}
	public Son(int age, String name) {
		super(age, name);// 调用父类的有参构造方法
	}
	
}
public class Test {
	public static void main(String[] args) {
		Son son = new Son(18, "xxx");
		System.out.println(son.getAge() + "," + son.getName());
	}
}
```

#### 2.5.2  this

##### 2.5.2.1 this关键字的用法

1. this访问本类成员变量

```java
class Father{
	int num = 20;
	
	public void method() {
		int num = 30;
		System.out.println("成员变量num的值：" + this.num);
		System.out.println("局部变量num的值：" + num);
	}
}

public class Test{
    public static void main(String[] args){
        
    }
}
```

2. this访问本类的成员方法

```java
class Father{

	public void method() {
		System.out.println("本类成员方法method()");
	}
    
	public void show() {
		System.out.println("本类成员方法show()");
		
		// 访问本类中的method方法
		this.method();
	}
}

public class Test1 {
	public static void main(String[] args) {
		Father father = new Father();
		father.show();
		
	}
}
```

3. this访问本类构造方法：this（）可以在本类的一个构造方法中，调用另一个构造方法

```java
class Father{
	int num;
	
	public  Father() {
		this(18);
		System.out.println("本类无参构造方法");
	}
    
	public Father(int num) {
		System.out.println("本类有参构造方法");
		this.num = num;
		
	}
}

public class Test1 {
	public static void main(String[] args) {
		Father father = new Father();
	}
}


```

#### 2.5.3 小结

```java
this关键字的三种用法：
	1.this访问本类成员变量
	2.this访问本类成员方法
	3.this访问本类构造方法
super关键字的三种用法：
	1.super访问父类成员变量
	2.super访问父类成员方法
	3.super访问父类的构造方法
		1.子类的构造方法会默认调用父类的空参构造
		2.super访问父类的构造方法，可以用来初始化从父类继承过来的属性
		3.在子类的构造方法中，使用super调用父类的构造方法，必须放在子类构造方法的第一行
```

### 2.6 继承体系对象内存图

每次创建子类对象时，先初始化父类空间，再创建子类对象本身

![](images\继承体系对象内存图.png)

### 2.7 继承的特点

1. java只支持单继承，就是一个子类只能有一个直接父类，但是父类可以有多个子类
2. 可以多层继承，就是一个子类只能有一个直接父类，可以由多个间接父类

**补充**：顶层父类Object类，所有的类默认继承Object类，作为父类的Java中所有的类都是直接继承或者是间接继承Object类，所有类都是Object类的子类

## 3、抽象类

抽象类是在普通类的结构里面**增加抽象方法**的组成部分

**抽象（abstract）：被abstract关键字修饰的类就是抽象类，抽象类中的抽象方法没有方法体**

**特点：**抽象类不能被创建对象，它就是**用来做父类的，被子类继承**

格式：

```java
修饰符 abstract class 类名{ // 定义一个抽象类
    成员变量
    构造方法
    成员方法 // 有方法体
        
    抽象方法 // 没有方法体，且使用abstract关键字修饰
}
```

```java
abstract class Animal{
    
}

public class Test{
    public static void main(String[] args){
        Animal animal = new Animal();// 报错，抽象类不能被创建对象
    }
}
```

### 3.1 抽象方法的概述与定义

**概述：**使用abstract修饰的方法，没有方法体的就是抽象方法

**作用：**强制要求子类重写

抽象方法的使用场景：**如果父类中某个方法，所有子类都有不同的实现，那么就可以把该方法定义为抽象方法**

定义：

```java
修饰符 abstract 返回值类型 方法名(参数)();
public abstract void show();
```

### 3.2  抽象类的注意事项

1. 抽象类**不能被创建对象**，抽象类就是用来用作父类，被子类继承
2. 抽象类虽然不可以被创建对象，但可以有构造方法：**为成员变量初始化**
3. **抽象类中可以没有抽象方法，但是抽象方法必须定义在抽象类中**
4. 子类继承抽象类后，必须**重写抽象类中所有的抽象方法**，否则子类也必须是一个抽象类
4. 抽象方法必须是public或者protected，缺省时默认public

## 4、模板设计模式

**设计模式的概述：**就是解决一些问题时的固定思路，代码设计思路的经验总结

**模板设计模式概述**：针对一些情况，在**父类中指定一个模板，然后根据具体情况，在子类中灵活的具体实现该模板**

```java
public abstract class AbstractClass{
    // 有方法体的方法：通用模板
    // 共同的且繁琐的操作
    public void baseOperation(){
       	// do something
    }
    
    // 没有方法体放入方法（抽象方法）：填充模板（需要子类重新实现）
    // 由子类定制的操作
    protected abstract void costomOperation();
}
```

### 4.1 模板设计模式的实现步骤

1. 定义抽象父类作为模板

2. 在父类中定义“模板方法”

3. 子类继承父类，重写抽象方法（填充模板）

4. 测试类

```java
例子：开车，新司机和老司机

public abstract class Driver{
    public void driverCar(){
        // 通用模板
        System.out.println("开门");
		System.out.println("点火");
		//姿势
		ziShi();
		System.out.println("刹车");
		System.out.println("熄火");
	}
    
    // 填充模板
    public abstract void ziShi();
}

public class NewDriver extends Driver{

	@Override
	public void ziShi() {
		System.out.println("双手紧握方向盘...");
	}
}


public class OldDriver extends Driver{
	@Override
	public void ziShi() {
		System.out.println("右手握紧方向盘，左手喝可乐");
	}
}

public class Test {
	public static void main(String[] args) {
		NewDriver d1 = new NewDriver();
		d1.driverCar();
		
		System.out.println("**********************");
		OldDriver d2 = new OldDriver();
		d2.driverCar();
	}
}
```

## 5、final关键字

**概述：**==不可变的。可以用来修饰类，方法，变量==

1. 修饰类时该类不能被继承
2. 修饰方法时该方法不能被重写
3. 修饰变量时该变量只能被赋值一次，不能被重复赋值

### 5.1 修饰类

当final修饰一个类时，表名这个类不能被继承，也就是说，如果一个类你永远不会让他被继承，就可以用final进行修饰。final类中的成员变量可以根据需要设为final，但是**final类中的所有成员方法都会被隐式的指定为final方法**

```java
// 格式
修饰符 final class 类名{
}


例子：
final class Father{
    
}

class Son extends Father{ // 直接报错，不能被继承
    
}
```

### 5.2 修饰方法

作用：将方法锁定，以防止继承类修改它的含义

```java
// 格式
修饰符 final 返回值类型 方法名(){
    
}

class Futher{
	public void method1() {
		
	}
	
	public final void method2() {
		
	}
}

class Son extends Futher{
	@Override
	public void method1() {
		// TODO Auto-generated method stub
		super.method1();
	}
	
	@Override
	public void method2() {// 编译报错，被final被修饰的方法，不能被重写
		// TODO Auto-generated method stub

	}
	
}

public class Test {

}
```

### 5.3 修饰变量

**局部变量** = 基本变量

基本类型的局部变量，被final修饰后，其**数值一旦在初始化之后就不能更改**

```java
public class Test {
	public static void main(String[] args) {
		//常量：常量名一般所有字母大写：
		final int NUM1 = 10;
		
		//num1 = 20;//被final修饰后，只能赋值一次，不能再更改
	}
}
```

**成员变量：**

1. 显示初始化

```java
public class FinalVariable{
    final int NUM = 10;
}
```

2. 构造方法初始化

```java
public class FinalVariable{
    final int NUM2;
    public FinalVariable(int NUM2){
        NUM2 = NUM2;
    }
    
    public FinalVariable(){
        this.NUM2 = 10;
    }
}
```

3. 局部变量-- 引用类型

引用类型的局部变量，被final修饰后，只能指向一个对象，地址不能再更改，但是不影响对象内部的成员变量值的修改

## 6、static关键字

static关键字是一个静态修饰符关键字，表示静态的意思，**可以修饰成员变量和成员方法以及代码块**

### 6.1 static关键字的作用

#### 6.1.1 static修饰成员变量

当static修饰成员变量时，该变量称为**类变量**，也叫静态变量，该类的每个对象都共享同一个变量的值，任何对象都可以更改该变量的值，也可以**在不创建该类对象的情况下使用该类变量**

定义格式：

```java
static 数据类型 变量名;
```

静态成员变量的访问方式：

```java
类名.静态成员变量名; // 推荐
对象名.静态成员变量名;
```

```java
class ChinesePeople {
	// 非静态成员变量
	String name;
	
	// 静态成员变量
	static String country;
	
	public ChinesePeople() {
		
	}

	public ChinesePeople(String name,String country) {
		this.name = name;
		this.country = country;
	}
}

public class Test {
	public static void main(String[] args) {
		ChinesePeople p1 = new ChinesePeople("冰冰","中国");
		System.out.println("姓名：" + p1.name + ",国籍：" + p1.country);
		
		ChinesePeople p2 = new ChinesePeople();
		System.out.println("姓名：" + p2.name + ",国籍：" + p2.country);
		
		p2.country = "中华人民共和国";
		System.out.println(p1.country + "," + p2.country);
		
	}
}

结果：
姓名：冰冰,国籍：中国
姓名：null,国籍：中国
中华人民共和国,中华人民共和国
```

```java
// 实例变量在创建对象时要获取内存，每个对象都具有实例变量的副本，如果实例变量被递增，不会反映到其他对象中
class Counter{
    // 实例变量
    int count = 0;
    
    public Counter(){
        count++;
        System.out.println(count);
    }
}

public class Test{
    public static void main(String[] args){
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        counter c3 = new Counter();
    }
}

执行结果：
1
1
1
```

```java
// 静态变量只获取一次内存，如果任何对象更改静态变量的值，其他对象可以访问同一变量值

class Counter{
    static int count = 0;
    
    public Counter(){
        count++;
        System.out.println(count);
    }
}

public class Test{
    public static void main(String[] args){
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        Counter c3 = new Counter();
    }
}

执行结果：
1
2
3
```

#### 6.1.2 static修饰成员方法

被static修饰的成员方法会变成**静态方法，也称类方法**，该静态方法可以使用类名直接调用

1. 静态方法属于类，而不是类的对象

2. 可以直接调用静态方法，而不需要创建类的实例

3. 静态方法可以访问静态变量，并可以更改静态变量的值

**格式：**

```java
修饰符 static 返回值类型 方法名(参数列表){
    
}
```

**访问方式：**

```java
类名.方法名;// 推荐
对象名.方法名(实参);
```

```java
class Calculate{
    static int cube(int x){
        return x * x * x;
    }
}

public class Test{
    public static void main(String[] args){
        int result = Calculate.cube(5);
        System.out.println(result);
    }
}
```

```java
class ChinesePeople {
	//非静态成员变量
	String name;
	
	//静态成员变量
	static String country;
	
	public ChinesePeople() {
		
	}

	public ChinesePeople(String name,String country) {
		this.name = name;
		this.country = country;
	}
	
	//非静态方法
	public void method1() {
		System.out.println("非静态方法...method1方法");
	}
	
	public void method2() {
		//非静态方法中可以访问一切成员变量和成员方法
		System.out.println("非静态方法...method2方法");
		System.out.println(name);
		System.out.println(country);
		method1();
		method4();
	}
	
	//静态方法
	public static void method3() {
		//静态方法中不能访问非静态成员变量和非静态成员方法
		//System.out.println("非静态的成员变量："+name);//编译报错
		//method1();//编译报错
		
		System.out.println("静态的成员变量：" + country);
		method4();
		
		System.out.println("静态方法  method3()");
	}
	
	public static void method4() {
		System.out.println("静态方法  method4()");
	}

}


public class Test {
	public static void main(String[] args) {
		ChinesePeople p1 = new ChinesePeople("冰冰","中国");
		System.out.println("姓名："+p1.name+",国籍："+p1.country);
		
		ChinesePeople p2 = new ChinesePeople();
		System.out.println("姓名："+p2.name+",国籍："+p2.country);
		
		p2.country = "中华人民共和国";
		System.out.println(p1.country+","+p2.country);
		
		System.out.println(ChinesePeople.country);
		
		
		ChinesePeople.method3();
		ChinesePeople.method4();
		
	}

}

结果：
姓名：冰冰,国籍：中国
姓名：null,国籍：中国
中华人民共和国,中华人民共和国
中华人民共和国
静态的成员变量：中华人民共和国
静态方法  method4()
静态方法  method3()
静态方法  method4()
```

##### 6.1.2.1 静态方法调用的注意事项

**静态方法只能直接访问静态成员变量和静态成员方法，静态方法中不能访问非静态成员变量和非静态成员方法**

非静态方法中可以访问一切成员变量和成员方法

静态方法中不能出现this和super关键字

##### 6.1.2.2 为什么Java的main方法是静态的

这是因为对象不需要调用静态方法，如果它是非静态方法，jvm首先要创建对象，然后调用main()方法，这将导致额外的内存分配的问题。

#### 6.1.3 static修饰代码块

Java中的静态块主要有两个作用：

1. 用于初始化静态数据成员
2. 它在类加载时在main方法之前执行

```java
class A1{
    static{
        System.out.println("static block is invoked");
    }
    public static void main(String[] args){
        System.out.println("Hello main");
    }
}

执行结果：
static block is invoke
Hello main
```

### 6.2 以后开发中static的应用

以后的项目中，通常会需要一些“全局变量”或者的工具方法，这些全局的变量和方法，可以单独定义在一个类中，并声明为static（静态的），可以很方便的通过类名访问。

工具类：

```java
public class Utils {
	// 全局变量
	public static final int WIDTH = 800;
	public static final int HEIGHT = 1800;
	
	// 全局方法
	// 查找数组中最大值
	public static int getArrayMax(int[] arr) {
		int max = arr[0];
		for (int i = 0; i < arr.length; i++) {
			if(arr[i] > max) {
				max = arr[i];
			}
		}
		
		return max;
	}
}
// 测试类
public class Test {
	public static void main(String[] args) {
		System.out.println(Utils.WIDTH);
		System.out.println(Utils.HEIGHT);
		
		int[] arr = {11,22,33,44};
		int max = Utils.getArrayMax(arr);
		System.out.println(max);	
	}
}
```

