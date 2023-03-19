<p align = "center" ><font size = 10， color = "#009999">常用API</font></p>

## 1、 Date类

java.util.Date类表示一个日期和时间，内部精确到毫秒

### 1.1 构造方法

```java
Date() 
      分配 Date 对象并初始化此对象，以表示分配它的时间（精确到毫秒）。
    
Date(long date) 
      分配 Date 对象并初始化此对象，以表示自从标准基准时间（称为“历元（epoch）”，即 1970 年 1 月 1 日 00:00:00 GMT）以来的指定毫秒数。
```

```java
import java.util.Date;

public class Test {
	public static void main(String[] args) {
		//创建当前系统时间对应的日期对象
		Date date1 = new Date();
		System.out.println(date1);//Fri Nov 11 16:39:15 CST 2022

		//创建以标准基准时间为基准，指定偏移1000毫秒
		Date date2 = new Date(1000);
		System.out.println(date2);//Thu Jan 01 08:00:01 CST 1970
		
		//创建日期对象，表示1970年1月1日07：59：59
		Date date3 = new Date(-1000);
		System.out.println(date3);//Thu Jan 01 07:59:59 CST 1970
	}
}
```

### 1.2 Date常用方法

```java
long getTime() 
      返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。 
          
void setTime(long time) 
      设置此 Date 对象，以表示 1970 年 1 月 1 日 00:00:00 GMT 以后 time 毫秒的时间点。 

boolean after(Date when) 
      测试此日期是否在指定日期之后。 
          
boolean before(Date when) 
      测试此日期是否在指定日期之前。
```

```java
import java.util.Date;

public class Test {
	public static void main(String[] args) {
		//创建当前时间对象的日期对象
		Date date1 = new Date();
		System.out.println(date1);//Fri Nov 11 16:56:13 CST 2022
		
		//创建以标准基准时间为基准，指定偏移1000毫秒
		Date date2 = new Date(1000);
		System.out.println(date2);//Thu Jan 01 08:00:01 CST 1970
		
		//获取当前时间日期对象距离标准基准时间的毫秒值：时间戳
		System.out.println(date1.getTime());//1668157016224
		System.out.println(date2.getTime());//1000
		
		//修改date1距离标准基准时间的毫秒值
		date1.setTime(2000);//
		System.out.println(date1);//Thu Jan 01 08:00:02 CST 1970
		
		////修改date2距离标准基准时间的毫秒值
		date2.setTime(2000);//
		System.out.println(date2);//Thu Jan 01 08:00:02 CST 1970
		
		//创建当前时间对应的日期对象
		Date date3 = new Date();
		System.out.println("date3的日期是否在date1之前："+date3.before(date1));//false
		System.out.println("date3的日期是否在date1之后："+date3.after(date1));//true
	}
}
```

## 2、DateFormat

DateFormat是日期/时间格式化子类的**抽象类**，通过这个类可以帮助我们完成日期和文本之间的转换，Date对象与String之间的来回转换

**格式化：**按照指定的格式，把Date对象转换成String对象

**解析：**按照指定的格式，将String对象转换为Date对象

### 2.1 SimpleDateFormat

simpleDateFormat是DateFormat的子类，是一个具体实现的类

#### 2.1.1 SimpleDateFormat构造方法

```java
SimpleDateFormat() 
	构造一个 SimpleDateFormat使用默认模式和日期格式符号为默认的 FORMAT区域设置。 
    
SimpleDateFormat(String pattern) // 常用
	使用给定模式 SimpleDateFormat并使用默认的 FORMAT语言环境的默认日期格式符号。  
```

| 标识字母（区分大小写）  | 含义 |
| ----------------------- | ---- |
| y（一般为 yyyy 表示年） | 年   |
| M（一般为MM表示月）     | 月   |
| d（一般用dd表示日）     | 日   |
| H（一般用HH表示小时）   | 时   |
| m（一般用mm表示分钟）   | 分   |
| s（一般用ss表示秒钟）   | 秒   |

#### 2.1.2 DateFormat类的常用方法

```java
String format(Date date) 
	将日期格式化成日期/时间字符串。
    
Date parse(String source) 
	从给定字符串的开始解析文本以生成日期。  
```

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Test1 {
	public static void main(String[] args) throws ParseException {
		// 把Date类型的对象转换为String类型
		// 创建当前日期的对象
		Date date = new Date();
		System.out.println(date);
		
		// 创建日期格式化对象，并且指定日期格式
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		
		// 使用日期格式化对象，把日期对象转换为String对象
		String dateStr = sdf.format(date);
		System.out.println(dateStr);
		
		
		System.out.println("=======================");
		// 把String类型的对象转换为Date对象
		String str = "2021年09月09日 12时12分12秒";
		
		// 创建日期格式
		SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒");
		
		// 解析:String转换为Date
		Date date1 = sdf1.parse(str);
		System.out.println(date1);// Thu Sep 09 12:12:12 CST 2021
	}
}
```

#### 1.1.3 练习（求出生到现在的天数）

需求：从键盘输入出生日期，打印出来到世界的天数

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

// 需求：从键盘输入出生日期，打印出已经来到这个世界的天数
public class Test1 {
	public static void main(String[] args) throws ParseException {
		// 创建输入对象
		Scanner sc = new Scanner(System.in);
		
		// 输入String类型的出生日期
		System.out.println("请输入你的出生日期（格式为yyyy-MM-dd）:");
		String birthdayStr = sc.next();
		
		// 将出生日期解析
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
		Date birthdayDate = sdf.parse(birthdayStr);
        // 得到生日时的时间戳
		long birthdayTime = birthdayDate.getTime();
		
		
		// 得到当前时间的时间戳
		Date date = new Date();
		long nowDateTime = date.getTime();
		
		// 进行相减处理
		System.out.println("你来到这个世界已经" + ((nowDateTime - birthdayTime)/1000/60/60/24) + "天");
		sc.close();
	}

}
```

## 3、Calendar

Calendar类表示一个日历类，**Calendar类是一个抽象类，不能创建对象**，可以使用它的直接子类**GregorianCalendar**进行创建对象

获取GregorianCalendar对象：

1. 直接创建对象的方式获取
2. 通过**Calendar的静态getInstance（）**方法获取GregorianCalendar对象

```java
方法：
static Calendar getInstance() 
	使用默认时区和区域设置获取日历。

boolean after(Object when) 
	返回 Calendar是否 Calendar指定时间之后的时间 Object 。  
    
boolean before(Object when) 
	返回此 Calendar是否 Calendar指定的时间之前指定的时间 Object 。  

int get(int field) 
	返回给定日历字段的值。  
    
void setTime(Date date) 
	使用给定的 Date 设置此 Calendar 的时间。 
```

```java
/* YEAR=2022, MONTH=10, 
 * WEEK_OF_YEAR=47, WEEK_OF_MONTH=3
 * DAY_OF_MONTH=18
 * DAY_OF_YEAR=322, DAY_OF_WEEK=6, DAY_OF_WEEK_IN_MONTH=3
 */
```

```java
import java.util.Calendar;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Test2 {
	public static void main(String[] args) throws Exception {
		// 创建当前时间
		Calendar cal = Calendar.getInstance();
		System.out.println(cal);
		
		/* 结果：
		 * java.util.GregorianCalendar[time=1668783580707,
		 * areFieldsSet=true,areAllFieldsSet=true,lenient=true,
		 * zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",
		 * offset=28800000,dstSavings=0,useDaylight=false,transitions=29,
		 * lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,
		 * YEAR=2022,MONTH=10,WEEK_OF_YEAR=47,WEEK_OF_MONTH=3,DAY_OF_MONTH=18,
		 * DAY_OF_YEAR=322,DAY_OF_WEEK=6,DAY_OF_WEEK_IN_MONTH=3,AM_PM=1,HOUR=10,
		 * HOUR_OF_DAY=22,MINUTE=59,SECOND=40,MILLISECOND=707,
		 * ZONE_OFFSET=28800000,DST_OFFSET=0]

		 */
		
		// 获取日历对象中的年/月/日
		
		/*YEAR=2022, MONTH=10, WEEK_OF_YEAR=47, WEEK_OF_MONTH=3, DAY_OF_MONTH=18,
		 * DAY_OF_YEAR=322, DAY_OF_WEEK=6, DAY_OF_WEEK_IN_MONTH=3
		 */
		int year = cal.get(Calendar.YEAR);// 年
		
		int month = cal.get(Calendar.MONTH);// 月
		
		int day = cal.get(Calendar.DAY_OF_MONTH);// 日
		
		System.out.println(year); // 2022
		System.out.println(month); // 10
		System.out.println(day); // 18
		
		System.out.println("====================");
		
		Calendar cal1 = Calendar.getInstance();
		String birthday = "2000年10月1日";
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日");
		Date birthdayDate = sdf.parse(birthday);
		
		cal1.setTime(birthdayDate);
		System.out.println(cal1.get(Calendar.YEAR)); // 2000
		System.out.println(cal1.get(Calendar.MONTH));// 9
		System.out.println(cal1.get(Calendar.DAY_OF_MONTH)); // 1
		
		
		// 创建当前日历时间
		Calendar cal2 = Calendar.getInstance();
		System.out.println("cal1是否早于cal2:" + cal1.before(cal2)); // true
		System.out.println("cal1是否晚于cal2:" + cal1.after(cal2)); // false
	}

}
```

## 4、Math类

Math类中包含用于执行基本数学运算的方法，如基本指数，对数，平方根和三角函数等

### 4.1 Math方法

```java
static int max(int a, int b) 
	返回两个 int值中的较大值， 其他数据类型同理

static int min(int a, int b)
    返回两个int值中得较小值，其他数据类型同理
  
static double abs(double a) 
	返回值为 double绝对值。  
    
static double ceil(double a) 
     向上取整
    
static double floor(double a) 
     向下取整

public static double pow(double a, double b) 
    获取a的b次幂
    
public static long round(double a)
    四舍五入
```

```java
public class MathDemo{
    public static void main(String[] args){
        // 最大值
        System.out.println(Math.max(12, 14));
        
        // 最小值
        System.out.println(Math.min(13, 67));
        
        // 绝对值
        System.out.println(Math.abs(-45));
        
        // 向上取整(double)
        System.out.println(Math.ceil(-4.56));
        
        // 向下取整(double)
        System.out.println(Math.floor(6.5));
        
        // 获取3的3次幂(double)
        System.out.println(Math.pow(3, 3));
        
        // 四舍五入(long)
        System.out.println(Math.round(-4.6));
    }
}
```

## 5、System类

java.lang.System，**可以获取与系统相关的信息**，不能被实例化

`System`类提供的`System`包括标准输入，标准输出和错误输出流

```java
static PrintStream  err 
	“标准”错误输出流。  
    
static InputStream in 
	“标准”输入流。  
    
static PrintStream out 
	“标准”输出流。  
```

### 5.1 常用方法

```java
static long currentTimeMillis() 
	返回当前时间（以毫秒为单位）。  
    
static void exit(int status) 
	终止当前运行的Java虚拟机。  
    
static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length) 
	将指定源数组中的数组从指定位置复制到目标数组的指定位置。  
```

```java
import java.util.Date;

public class Test4 {
	public static void main(String[] args) {
		System.out.println("开始运行程序");
		
		// System.exit(0); // 程序正常退出
		// System.exit(-1); // 程序非正常退出
		
		// 获取当前时间距离标准时间的毫秒值
		Date date = new Date();
		long time = date.getTime();
		System.out.println(time); // 1668909145284
		System.out.println(System.currentTimeMillis()); // 1668909145285
		
		int[] arr1 = {1, 2, 3, 4, 5, 6};
		int[] arr2 = {10, 20, 30, 40, 50, 60};
		
		// 利用System.arraycopy()将arr1中的3， 4， 5， 6元素拷贝到arr2数组中{10，3， 4，5，6，60}
		System.arraycopy(arr1, 2, arr2, 1, 4);
		
		System.out.println(arr2); // 地址值
		
		// 遍历arr2
		for (int i = 0; i < arr2.length; i++) {
			System.out.print(arr2[i] + ","); // 10, 3, 4, 5, 6, 60
		}
	}
}
```

### 5.2 练习

打印1-10000需要花费的时间

```java
public class PrintNum{
    public static void main(String[] args){
        
        long start = System.currentTimeMillis();
        
        // 打印1-10000
        for (int i = 1; i <= 10000; i++){
            if (i % 100 == 0){
                System.out.println();
            } else{
                System.out.print(i);
            }    
        }
        long end = System.currentTimeMillis();
        
        System.out.println("打印1-10000总共花费：" + (end - start) + "ms"); // 46ms
    }
}
```

## 6、BigDecimal

因为我们的计算机是二进制的，浮点数没办法用二进制进行精确表示

```java
public class Test6 {
	public static void main(String[] args) {
		System.out.println(0.09 + 0.01);
		System.out.println(0.3 - 0.14);
		System.out.println(1.337 / 10);
		System.out.println(3.0 * 5.6);
	}

}

结果：
0.09999999999999999
0.15999999999999998
0.13369999999999999
16.799999999999997
```

**cup表示浮点数由指数和位数两部分组成**

例如：2.4的二进制表示是：2.3999999999999

在大多数的计算中，一般采用**java.math.BigDecimal**类来计算

==注意事项==：

1. **对于浮点数运算，不要使用基本数据类型，使用BigDecimal类来计算**
2. BigDecimal 类进行计算，提供了更加精准的数据计算方式

### 6.1 构造方法

```java
BigDecimal(double val) 
    将 double 转换为 BigDecimal，后者是 double 的二进制浮点值准确的十进制表示形式。
    
BigDecimal(double val, MathContext mc) 
	将 double转换为 BigDecimal ，根据上下文设置进行舍入。 
    
BigDecimal(String val) //推荐使用
    将 BigDecimal 的字符串表示形式转换为 BigDecimal。
    
BigDecimal(String val, MathContext mc) 
	一个转换的字符串表示 BigDecimal成 BigDecimal ，接受相同的字符串作为 BigDecimal(String)构造，利用根据上下文设置进行舍入。 
```

### 6.2 常用方法

```java
BigDecimal abs() 
	返回一个 BigDecimal ，其值为此 BigDecimal的绝对值，其缩放比例为 this.scale() 。  
    
BigDecimal add(BigDecimal augend) 
	返回 BigDecimal ，其值是 (this + augend) ，其标为 max(this.scale(), augend.scale()) 。
BigDecimal subtract(BigDecimal subtrahend) 
    返回一个 BigDecimal，其值为 (this - subtrahend)，其标度为 max(this.scale(), subtrahend.scale())。 
    
BigDecimal multiply(BigDecimal multiplicand) 
    返回一个 BigDecimal，其值为 (this × multiplicand)，其标度为 (this.scale() + multiplicand.scale())。 
    
BigDecimal divide(BigDecimal divisor) 
    返回一个 BigDecimal，其值为 (this / divisor)，其首选标度为 (this.scale() - divisor.scale())；如果无法表示准确的商值（因为它有无穷的十进制扩展），则抛出 ArithmeticException。 
    
BigDecimal divide(BigDecimal divisor, int scale, RoundingMode roundingMode) 
	返回一个 BigDecimal ，其值为 (this / divisor) ，其比例为指定。 
    divisor ：除数对应的BigDecimal对象
    scale：精确的位数
    RoundingMode.HALF_DOWN：四舍五入
```

```java
import java.math.BigDecimal;
import java.math.RoundingMode;

public class Test6 {
	public static void main(String[] args) {
		// 加减相似
		BigDecimal num1 = new BigDecimal("0.09");
		BigDecimal num2 = new BigDecimal("0.01");
		BigDecimal sum = num1.add(num2);
		System.out.println(sum); // 0.10
		
		
		// 乘
		BigDecimal num3 = new BigDecimal("5.4");
		BigDecimal num4 = new BigDecimal("3.33");
		BigDecimal multiply = num3.multiply(num4);
		System.out.println(multiply);// 17.982
		
		// 除
		BigDecimal num5 = new BigDecimal("10");
		BigDecimal num6 = new BigDecimal("3");
		// BigDecimal divide1 = num3.divide(num4);
		// System.out.println(divide1); 
		//  除不尽就会报：java.lang.ArithmeticException: Non-terminating decimal expansion
		
		// public BigDecimal divide(BigDecimal divisor, int scale, RoundingMode roundingMode)
        // divisor ：除数对应的BigDecimal对象
        // scale：精确的位数
        // RoundingMode.HALF_DOWN：四舍五入
		BigDecimal divide2 = num5.divide(num6, 2, RoundingMode.HALF_DOWN);
		System.out.println(divide2); // 3.33
		
	}

}
```

## 7、包装类

### 7.1 包装类的概述

Java提供了两个类型系统。基本类型与引用类型，如果我们想要让基本类型向对象一样操作，就可以使用基本类型对应的包装类。

| 基本类型 | 对应的包装类型(位于java.lang中) |
| -------- | ------------------------------- |
| byte     | Byte                            |
| short    | Short                           |
| int      | **Integer**                     |
| long     | Long                            |
| float    | Float                           |
| double   | Double                          |
| char     | **Character**                   |
| boolean  | Boolean                         |

### 7.2 Integer类

#### 7.2.1 构造方法以及静态方法

```java
Integer(int value) 
	构造一个新分配的 Integer对象，该对象表示指定的 int值。  

Integer(String s) 
	构造一个新分配 Integer对象，表示 int由指示值 String参数。  

static Integer valueOf(int i) 
	返回一个表示指定的 int 值的 Integer 实例。
          
static Integer valueOf(String s) 
	返回保存指定的 String 的值的 Integer 对象。 
```

```java
public class Test{
    public static void main(String[] args){
        // int ---> Integer
        Integer num1 = new Integer(10);
        Integer num2 = Integer.valueOf(10);
        
        // String ---> Integer
        Integer num3 = new Integer("20");
        Integer num4 = Integer.valueOf("20");
        
        // Integer ---> int
        int num5 = num1.intValue();
        int num6 = num3.intValue();
    }
}
```

### 7.3 拆箱和装箱

**装箱：从基本数据类型转换为对应的包装类**

**拆箱：从包装类对象转换为对应的基本类型**

```java
public class Test{
    public static void main(String[] args){
        // 装箱：int ---> Integer
        Integer num1 = new Integer(10);
        Integer num2 = Integer.valueOf(10);
   
        // 拆箱：Integer ---> int
        int num3 = num1.intValue();
        int num4 = num2.intValue();
        
        // 自动装箱与拆箱
        /*自动装箱：从基本类型自动转换为对应的包装类对象
		 *自动拆箱:从包装类对象自动转换为对应的基本类型
		 */
        
        // 自动装箱
        Integer num5 = 10;
        
        // 自动拆箱
        int num6 = num5;
    }
}
```

