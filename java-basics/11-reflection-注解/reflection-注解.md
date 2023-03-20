<p align = "center" ><font size = 6， color = "#009999">reflection & 注解</font></p>

[toc]

## 1、反射

### 1.1 类的加载

​	当我们的程序在运行之后，第一次使用某个类的时候，会将此类的.class文件读取到内存中，并将此类的所有信息存储到一个class对象中

类的加载时机：

1. 创建类的实例

2. 类的静态变量，或者为静态变量复制

3. 类的静态方法

4. 使用反射方式强制创建某个类或者接口对应的class对象

5. 初始化某个类的对象

6. 直接使用java.exe命令运行某个类

   以上6中情况中任意一种，都可以导致jvm将一个类加载到方法区

### 1.2 类加载器

类加载器是负责**将磁盘上的.class文件读取到内存并且生成Class对象**

==获取类加载器：类的字节码对象 .getClassLoader()==

```java
public class Test{
    public static void main(String[] args){
        // 类的字节码对象
        // 获取test类的类加载器
        // 获取类加载器：类的字节码对象
        ClassLoader c1 = Test.class.getClassLoader();
        System.out.println(c1);
    }
}
```

### 1.3 Class对象的获取方式

1. 通过类名.class获取

2. 通过对象名.getClass获取

3. 通过Class类的静态方法：static Class for Name("类全名")；

   ​	每个类的class对象只有一个

```java
public class Test {
	public static void main(String[] args) throws Exception {
        // 创建Class对象 
        // 方式1
		Class<Student> c1 = Student.class;
		
        // 方式2
		Student stu = new Student();
		Class<? extends Student> c2 = stu.getClass();
		
        // 方式3
		Class<?> c3 = Class.forName("net.wanhe.day14.Student");
		
		System.out.println(c1);
		System.out.println(c2);
		System.out.println(c3);
		System.out.println(c1 == c2);
	}

}
```



#### 1.3.1 Class类中的常用方法

```java
String getSimpleName()
    获得类名字字符串，类名
    
String getName()
    获得类全名：包名 + 类名
    
T newInstance()
    创建Class对象关联类的对象
```

```java
public class Test {
	public static void main(String[] args) throws Exception {
		Class<Student> c1 = Student.class;
		
		Student stu = new Student();
		Class<? extends Student> c2 = stu.getClass();
		
		Class<?> c3 = Class.forName("net.wanhe.day14.Student");
		
		System.out.println(c1);
		System.out.println(c2);
		System.out.println(c3);
		System.out.println(c1 == c2);
		
		// 获取类名字字符串
		String simpleName = c1.getSimpleName();
		System.out.println(simpleName); // Student
		
		// 获取类全名
		System.out.println(c1.getName());
		
		// 创建Student类的对象
		Student stu1 = c1.newInstance(); // 其实就是相当于调用了Student类的空参构造方法
	    System.out.println(stu1);
	}

}
```

### 1.4 反射操作构造方法

```java
反射操作构造方法：
    获得Constructor对象来创建类的对象
    
Constructor类的概述：
    类中的，每一个构造方法，都是一个Constrctor类的对象
```

#### 1.4.1 通过反射获取类的构造方法

```java
Constructor<?>[] getConstructors() 
	返回包含一个数组 Constructor对象反射由此表示的类的所有公共构造 类对象。  
    获取类中所有的构造方法，只能是public的
    
Constructor<T> getConstructor(类<?>... parameterTypes) 
	返回一个 Constructor对象，该对象反映 Constructor对象表示的类的指定的公共 类函数。 
    只能获取public修饰的构造方法
    
Constructor<T> getDeclaredConstructor(类<?>... parameterTypes) 
	返回一个 Constructor对象，该对象反映 Constructor对象表示的类或接口的指定 类函数。 
    public，protected，默认，private修饰符的构造方法
    
Constructor<?>[] getDeclaredConstructors() 
	返回一个反映 Constructor对象表示的类声明的所有 Constructor对象的数组 类 。  
    public，protected，默认，private修饰符的构造方法
```

```java
T newInstance(Object... initargs) 
	使用此 Constructor对象表示的构造函数，使用指定的初始化参数来创建和初始化构造函数的声明类的新实例。  

public void setAccessible(boolean flag)
    设置“暴力反射”，是否取消权限检查。
```

```java
// Student类
public class Student {
	private String name;
	private int age;
	
	
	// 无参
	public Student() {
		
	}
	
	private Student(int age) {
		
		this.age = age;
	}

	public Student(String name) {
		this.name = name;
	}
	
	// 满参
	public Student(String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	public String toString(){
		return "[" + this.age + "," + this.name +"]";
	}
}
```

```java
// Test类
import java.lang.reflect.Constructor;

public class Test {
	public static void main(String[] args) throws Exception {
		// 获取Student类的Class对象
		Class<Student> c1 = Student.class;
		
		// 获取单个构造方法
		// 获取无参的构造方法,非私有
		Constructor<Student> con1 = c1.getDeclaredConstructor();
		System.out.println(con1);
		
		// 获取满参构造
		Constructor<Student> con2 = c1.getDeclaredConstructor(String.class, int.class);
		System.out.println(con2);
		
		// 获取私有构造方法
		Constructor<Student> con3 = c1.getDeclaredConstructor(int.class);
		System.out.println(con3);
		
		System.out.println("==========================");
		Constructor<?>[] arr1 = c1.getDeclaredConstructors();
		for (Constructor<?> con : arr1) {
			System.out.println(con);
		}
		
		System.out.println("==========================");
		// 通过con1（无参）表示的构造方法来创建对象
		Student stu1 = con1.newInstance();
		System.out.println(stu1);
		
		Student stu2 = con2.newInstance("李毅", 23);
		System.out.println(stu2);
		
		// 取消con3表示的构造方法的权限检查
		con3.setAccessible(true);
		Student stu3 = con3.newInstance(19);
		System.out.println(stu3);		
	}

}
```

### 1.5 反射操作成员方法

``` java
public class Student1 {
	public void show1() {
		System.out.println("show1....方法");
	}
	
	public void show2(int num) {
		System.out.println("show2....方法");
	}
	
	public void show3() {
		System.out.println("show3....方法");
	}
	
	public void show4() {
		System.out.println("show4....方法");
	}
	
	public int show5(int num) {
		System.out.println("show5....方法");
		return 100;
	}

}
```

```java
import java.lang.reflect.*;

public class Test1 {
	public static void main(String[] args) throws Exception {
        // 创建Student类的class对象
		Class<Student1> c = Student1.class;
		
		// 获取所有的构造方法
		Constructor<?>[] cons = c.getDeclaredConstructors();
		
		Student1 stu = null;
		
		for (Constructor<?> con : cons) {
			stu = (Student1)con.newInstance();
		}
		
		// 获取所有的成员方法
		Method[] methods = c.getDeclaredMethods();
		
		// 遍历所有的成员方法
		for (Method m : methods) {
			if(m.getName().equals("show1")){
				m.invoke(stu);
			}
			
			if(m.getName().equals("show2")){
				m.invoke(stu, 20);
			}
			
			if(m.getName().equals("show5")){
				Object res = m.invoke(stu, 20);
				System.out.println(res);
			}
			
		}
	} 

}
```

### 1.6 反射操作成员变量

```java
public class Student2 {
	String name;
	private int age;

}
```

```java
import java.lang.reflect.Field;

public class Test2 {
	public static void main(String[] args) throws Exception {
		Class<Student2> c = Student2.class;
		
		Student2 stu = c.newInstance();
		
		// 获取单个成员变量
		Field f1 = c.getDeclaredField("name");
		System.out.println(f1);
		
		
		Field f2 = c.getDeclaredField("age");
		System.out.println(f2);
		
		System.out.println("===================");
		
		Field[] arr = c.getDeclaredFields();
		for (Field field : arr) {
			System.out.println(field);
		}
		
		System.out.println("====================");
		
		// 获取属性的类型
		System.out.println(f1.getType());
		System.out.println(f2.getType());
		
		System.out.println("=====================");
		f1.set(stu, "张三");
		
		f2.setAccessible(true);
		f2.set(stu, 16);
		
		System.out.println("======================");
		// 获取属性的值
		// 通过反射获取f1表示的name属性
		System.out.println(f1.get(stu));
		System.out.println(f2.get(stu));
 	}

}
```

## 2、注解

### 2.1 概念

注解是代码级别的说明，和我们学的类，接口是平级关系

注解相当于一种标记，在程序中加入注解就相当于为程序做了一个标记，程序就根据标记去认识并做相对应的事情

### 2.2 JDK提供的三种基本注解

@Override：描述方法的重写

@SuppressWarning：压制，忽略警告

@Deprecated：标记过时

```java
public class Test{
    public static void main(String[] args){
        @SuppressWarnings("all")
    	int num;
    }
    
    @Deprecated
    public static void method1(){
        
    }
    
    public static void method2(){
        
    }
    
}
```

### 2.3 自定义注解

语法：

```java
public @interface 注解名{
    
}
```

```java
/*
定义注解
*/
public @interface Annotation1 {
	// 1. 基本数据类型
	int a();
	double b();
	
	// 2. String类型
	String c();
	
	// 3. class类型
	Class d();
	
	// 4. 注解类型
	Annotation f();
	
	// 5. 枚举类型
	Sex e();
	
	// 6. 以上类型的一维数组类型
	int[] g();
	String[] h();
	Sex[] i();

}
```

### 2.4 使用注解并给注解的属性赋值

```java
使用：
    如果一个注解中有属性，那么使用注解的时候一定要给注解属性赋值
    如果一个注解中没有属性，那么使用注解的时候不需要给属性赋值,直接使用即可
    
给注解的属性赋值
    @注解名(属性名1=值1， 属性名2=值2)
```

```java
// 无属性
public @interface Annotation {

}

// 有属性
public @interface Annotation1 {
	String name();
	int age();
	String[] arr();

}

// 测试类
@Annotation
@Annotation1(name="张三",age=18, arr = {"123", "abc"}) // 不给属性赋值会报错
public class Test {
	@Annotation
	@Annotation1(name="张三",age=18, arr = {"123", "abc"})
	public static void main(String[] args) {
		@Annotation
		@Annotation1(name="张三",age=18, arr = {"123", "abc"})
		int num = 10;
	}

}
```

#### 2.4.1 注意事项

```java
@interface Annotation1{
	int[] arr();
}

@interface Annotation2{
	String value();
}

@interface Annotation3{
	String[] value();
}

@interface Annotation4{
	String[] value() default {"good", "ye"};
	int num() default 10;
}

public class Test {
	public static void main(String[] args) {
		
	}
	
	// 属性是一维数组且数组的值只有一个的时候，可以省略{}
	@Annotation1(arr = {10})
	// @Annotation1(arr = 10)
	public void show1() {
		
	}
	
	// 只有一个属性且属性名为value，可以省略value
	@Annotation2(value = "xxx")
	// @Annotation2("xxx")
	public void show2() {
			
	}
	
	@Annotation3(value = {"xxx", "123"})
	// @Annotation3({"xxx", "123"})
	// @Annotation3({"xxx"})
	// @Annotation3("xxx")
	public void show3() {
				
	}

	@Annotation4(value = {"123"}, num = 10)
	// @Annotation1(arr = 10)
	public void show4() {
		
	}
}
```

### 2.5 元注解

定义在注解上的注解，限制注解的使用范围

**常用元注解：**

==**@Target：表示该注解作用在什么上面，默认注解可以是任何位置**==

METHOD：方法

TYPE：类，接口

FIELD：字段

CONSTRUCTOR：构造方法声明

==**@Retention：定义该注解保留到哪个代码阶段**==

SOURCE：只在源码上

CLASS：在源码和字节码上保留

RUNTIME：在所有阶段保留 

**.java(源码阶段)--->编译--->.class(字节码阶段)--->加载内存--->运行（Runtime）**

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation1{
	
}

@MyAnnotation1
public class Test2 {
	public static void main(String[] args) {
		// @MyAnnotation1 // 报错
		String str;
	}

}
```

### 2.6 注解解析

```java
import java.lang.reflect.Method;
import java.util.Arrays;

@MyAnnotation(names= {"张李"},age=18)
public class Test {
	public static void main(String[] args) throws Exception, SecurityException {
		Class<Test> c = Test.class;
		//获取class对象上的注解
		MyAnnotation myAnnotation = c.getAnnotation(MyAnnotation.class);
		
		//根据注解获取该注解的属性值
		String[] names = myAnnotation.names();
		System.out.println(Arrays.toString(names));//[张李]
		
		int age = myAnnotation.age();
		System.out.println(age);//18
		
		System.out.println("****************************");
		//需求：获取show1方法上的注解，并且获取该注解的值
		//获取show1方法的method对象
		Method m = c.getDeclaredMethod("show1");
		
		//获取方法上的注解
		MyAnnotation annotation = m.getAnnotation(MyAnnotation.class);
		
		//根据注解获取属性值
		System.out.println(Arrays.toString(annotation.names()));//[李四]
		System.out.println(annotation.age());//19
		
		System.out.println("***************************************");
		//需求：判断Test方法中是否包含@MyAnnotation注解
		//获取show2方法的mathod对象
		Method m2 = c.getDeclaredMethod("show2");
		
		//判断方法是否包含注解
		System.out.println(m2.isAnnotationPresent(MyAnnotation.class));//false
		System.out.println(m.isAnnotationPresent(MyAnnotation.class));//true
	}
	
	@MyAnnotation(names= {"李四"},age=19)
	public void show1() {
		
	}
	
	public void show2() {
		
	}
}
```

### 2.7 完成注解的Test测试案例

在一个类中（TestDemo测试类)中有三个方法，其中两个方法上有@MyTest，另一个没有，还有一个主测试类（MainTest）中有一个main方法，在main方法中，让TestDemo类中含有@MyTest方法执行，自定义@MyTest，模拟单元测试

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyTest{
    
}
```

```java
public class TestDemo{
    @MyTest
    public void method1(){
        System.out.println("method1开始运行");
    }
    
    
    public void method2(){
        System.out.println("method2开始运行");
    }
    
    @MyTest
    public void method3(){
        System.out.println("method3开始运行");
    }
}
```

```java
public class MainTest{
	public static void main(String[] args){
        // 获取TestDemo的class对象
        Class<TestDemo> c = TestDemo.class;
        TestDemo testDemo = c.newInstance();
        
        // 获取该字节码对象中的所有方法
        Method[] arr = c.getMethods();
        
        // 遍历所有方法
        for (Method m : arr){
            // 判断遍历出来的方法是否有MyTest，如果有，就执行该方法
            if(m.isAnnotationPresent(MyTest.class)){
                m.invoke(testDemo);
            }
        }
        
    }
}
```

