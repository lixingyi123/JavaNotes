<p align = "center" ><font size = 10， color = "#009999">jdbc & 连接池</font></p>

## 1、JDBC

### 1.1 JDBC概述

JDBC：Java database connectivity: SUN公司为了简化Java与同意Java连接数据库，定义的一套规范

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/15-jdbc-%E8%BF%9E%E6%8E%A5%E6%B1%A0/images/jdbc%E6%A6%82%E8%BF%B0.png?raw=true)

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.mysql.jdbc.Driver;

public class Test {
	public static void main(String[] args) throws Exception {
		
		// 1.创建项目,拷贝jar包
		// 2.注册驱动
		// 方式1：DriverManager.registerDriver(new Driver());
		// 方式2：
		Class.forName("com.mysql.jdbc.Driver");
		String url = "jdbc:mysql://localhost:3306/day16";
		String user = "root";
		String password = "123456";
		
		// 3.获取连接
		Connection connection = DriverManager.getConnection(url, user, password);
		
		// 4.创建执行sql的对象
		Statement statement = connection.createStatement();
		
		
		// 5.执行sql，处理结果
		String sql = "select * from tb_teacher";
		ResultSet rs = statement.executeQuery(sql);
		
		
		while (rs.next()) {
			System.out.println("======================");
			System.out.println(rs.getInt("id"));
		}
		
		// 6.释放资源
		if (rs != null) {
			rs.close();
		}
		
		if (statement != null) {
			statement.close();
		}
		if (connection != null) {
			connection.close();
		}
	}

}
```

### 1.2 DriverManager

```java
方法1：
DriverManager.registerDriver(new Driver());

方式2：
Class.forName("com.mysql.jdbc.Driver");
```

### 1.3 Connection接口

1. 接口的实现在数据库的驱动中，所有与数据库的交互都是基于连接对象的
2. 创建执行sql语句，创建预编译执行sql对象

### 1.4 Statement

用来操作sql语句，并返回相应的结果

```java
ResultSet executeQuery(String sql) throws SQLException;只能执行select语句
int executeUpdate(String sql) throws SQLException;根据执行的DML语句，返回受影响的行数，执行增删改
```

### 1.5 ResultSet接口

1. 封装结果，查询结果的对象

提供一个游标，默认游标指向结果集的第一行之前

调用一次next，游标向下移动一行，提供一些get方法

### 1.6 JDBC增删改查

```java
// 查询
String sql = "select * from tb_teacher";
ResultSet rs = statement.executeQuery(sql);
		
while (rs.next()) {
	System.out.println("======================");
	System.out.println(rs.getInt("id"));
}

// 增删改
String sql = "update teacher set sex = 1 where name = '李玉'";
String sql = "delete from teacher where name = '李艺'";
String sql = "insert into teacher values(null, '李阳', 1, 46)";
int row = statement.executeUpdate(sql);
System.out.println("受影响的行数：" + row);
```

### 1.7 将数据封装到Teacher对象中

```java
// teacher类
public class Teacher {
	private int id;
	private String name;
	private boolean sex;
	private int age;
	
	
	public Teacher() {
		
	}
	
	public Teacher(int id, String name, boolean sex, int age) {
		super();
		this.id = id;
		this.name = name;
		this.sex = sex;
		this.age = age;
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

	public boolean getSex() {
		return sex;
	}

	public void setSex(boolean sex) {
		this.sex = sex;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}
	
    @Override
	public String toString() {
		return "id:" + this.id + "\nname:" + this.name + "\npassword:" + this.password; 
	}
	
}
```

### 1.8 JDBC工具类的抽取

```java
// db.properties文件
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/day16
username=root
password=123456
```

```java
// JDBC工具包
import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Properties;

public class JDBCUtils {
	private static String driver;
	private static String url;
	private static String username;
	private static String password;
	
	
	static{
		// 创建properties对象
		try {
			Properties pro = new Properties();
			InputStream is = JDBCUtils.class.getClassLoader().getResourceAsStream("db.properties");
			pro.load(is);
			url = pro.getProperty("url");
			username = pro.getProperty("username");
			password = pro.getProperty("password");
			driver = pro.getProperty("driver");
			
			Class.forName(driver);
			
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		
	}
	
	
	// 获得连接
	public static Connection getConnection() throws Exception{
		Connection connection = DriverManager.getConnection(url, username, password);
		return connection;
	}
	
	
	// 释放资源
	public static void release(ResultSet resultSet, Statement statement, Connection connection) throws Exception {
		if (resultSet != null) {
			resultSet.close();
		}
		
		if (statement != null) {
			statement.close();
		}
		if (connection != null) {
			connection.close();
		}
	}
}
```

```java
// 测试类
import java.sql.Connection;
import java.sql.Statement;

public class Test2 {
	public static void main(String[] args) throws Exception {
	
		Connection connection = JDBCUtils.getConnection();
		Statement statement = connection.createStatement();
		
		// 创建执行sql得到语句对象
		String sql = "update teacher set sex = 1 where name = '李玉'";
		int row = statement.executeUpdate(sql);
		System.out.println("受影响的行数：" + row);
		
		JDBCUtils.release(null, statement, connection);
		
	}

}
```

### 1.9 登录案例

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Scanner;

public class Test2 {
	public static void main(String[] args) throws Exception {
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入用户名：");
		String userName = sc.next();
		System.out.println("请输入密码：");
		String userPassword = sc.next();
		
		Connection connection = JDBCUtils.getConnection();
		Statement statement = connection.createStatement();
		
		
		
		String sql = "select id, name, password from user where name = '"+userName+"' and password = '"+userPassword+"'";
		ResultSet rs = statement.executeQuery(sql);
		
		User user = null;

		while (rs.next()) {
			user = new User();
			System.out.println("======================");
			user.setId(rs.getInt("id"));
			user.setName(rs.getString("name"));
			user.setPassword(rs.getString("password"));
		}

		JDBCUtils.release(null, statement, connection);
		
		if (user == null) {
			System.out.println("登录失败");
		}else {
			System.out.println("登录成功");
		}
	}

}
'or'1 '=' 1
```

### 1.10 sql注入问题出现

**问题：**当输入密码为：'or'1 '=' 1时，总能登录成功

把用户输入的or当成关键字注入到sql语句中

### 1.11 解决sql注入问题

#### 1.11.1 preparedStatement

预编译sql语句对象，是Statement接口的子接口

特点：性能比Statement高

会把sql语句先编译，格式固定好

会过滤用户输入的关键字

#### 1.11.2 用法

connection.preparedStatement(String sql)：创建preparedStatement对象

sql中如果有参数，通过？来进行占位

```java
select * from user where username = ? and password = ?
```

设置参数

```
setString(1, "李玉");
setString(2, "123456");
```

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Scanner;

public class Test2 {
	public static void main(String[] args) throws Exception {
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入用户名：");
		String userName = sc.next();
		System.out.println("请输入密码：");
		String userPassword = sc.next();
		
		Connection connection = JDBCUtils.getConnection();
		
		String sql = "select name, password from user where name = ? and password = ?";
		PreparedStatement ps = connection.prepareStatement(sql);
		ps.setString(1, userName);
		ps.setString(2, userPassword);
		
		// 执行sql语句
		ResultSet rs = ps.executeQuery();
		User user = null;

		while (rs.next()) {
			user = new User();
			System.out.println("======================");
			// user.setId(rs.getInt("id"));
			user.setName(rs.getString("name"));
			user.setPassword(rs.getString("password"));
		}

		JDBCUtils.release(rs, ps, connection);
		
		if (user == null) {
			System.out.println("登录失败");
		}else {
			System.out.println("登录成功");
		}
	}

}
```

## 2、连接池

Connction对象在jdbc使用的时候就会去创建对象，使用结束后将对象销毁，每次创建和使用对象都是耗时的操作，使用连接池对其进行优化

程序初始化的时候，初始化多个对象，将多个连接放入池中，每次取得时候，直接从池中获取，使用结束后，将连接归还到池中

### 2.1 连接池的原理

1. 程序一开始就创建一定数量的连接，放入一个容器中，这个容器我们就称为连接池
2. 使用的时候直接从连接池中取一个已经创建好的连接对象，使用完成之后，归还到池中
3. 如果池中的连接使用完了，还有程序需要使用连接，先等待一段时间，如果在这段时间之内有连接归还就去使用连接，没有连接归还，就创建一个新的连接，但是新创建的这一个连接不会归还
4. 集合一般选择：LinkedList

### 2.2 自定义连接池

```java
// 自定义连接池
import java.sql.Connection;
import java.util.LinkedList;

public class MyDateSource {
    // 定义LinkedList集合，用来存储初始化的连接
	private static LinkedList<Connection> list = new LinkedList<>();
	
	
	// 初始化5个连接，并存储到集合中
	static {
		for (int i = 0; i < 5; i++) {
			try {
				// 获得连接并放入list中
				Connection connection = JDBCUtils.getConnection();
				list.add(connection);
			} catch (Exception e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
		}
	}
	
	// 定义方法，用于获得连接
	public Connection getConnection() {
		Connection connection = list.removeFirst();
		return connection;
	}
	
	// 定义方法，用来归还连接
	public void addBack(Connection connection) {
		list.addLast(connection);
	}
	
	// 定义方法，获得连接池的数量
	public static int getCount() {
		return list.size();
	}

}
```

```java
// 测试类
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class Test {
	public static void main(String[] args) throws Exception {
		MyDateSource dateSource = new MyDateSource();
		
		Connection connection = dateSource.getConnection();
		String sql = "select * from user where id = ?";
		
		PreparedStatement statement = connection.prepareStatement(sql);
		statement.setInt(1, 2);
		ResultSet rs = statement.executeQuery();
		
		while (rs.next()) {
			System.out.println(rs.getInt("id"));
			System.out.println(rs.getString("name"));
		}
		
		System.out.println("获得连接之后：" + MyDateSource.getCount());
		dateSource.addBack(connection);
		JDBCUtils.release(rs, statement, null);
		System.out.println("归还连接之后：" + MyDateSource.getCount());
		
	}

}
```

### 2.3 第三方连接池

1. C3P0是一个开源免费的第三方连接池，有自动归还回收空闲连接的功能

```java
/*
 *C3P0工具类
 */ 
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.mchange.v2.c3p0.ComboPooledDataSource;

public class C3P0Utils {
	private static final ComboPooledDataSource DATA_SOURCE = new ComboPooledDataSource();
	
	/**
	 * 
	 * 获得连接的方法
	 * 
	 **/
	public static Connection getConnection() throws Exception{
		return DATA_SOURCE.getConnection();
	}
	
	
	/**
	 * 
	 * 释放资源
	 *
	 **/
	public static void release(ResultSet resultSet, Statement statement, Connection connection) throws Exception {
		if (resultSet != null) {
			resultSet.close();
		}
		
		if (statement != null) {
			statement.close();
		}
		if (connection != null) {
			connection.close();
		}
	}
}
```

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;


import com.mchange.v2.c3p0.ComboPooledDataSource;

public class Test {
	public static void main(String[] args) throws Exception {
		
		Connection connection = C3P0Utils.getConnection();
		String sql = "select * from user where id = ?";
		
		PreparedStatement statement = connection.prepareStatement(sql);
		statement.setInt(1, 2);
		ResultSet rs = statement.executeQuery();
		
		while (rs.next()) {
			System.out.println(rs.getInt("id"));
			System.out.println(rs.getString("name"));
		}
		
		C3P0Utils.release(rs, statement, null);
		
	}

}
```

2. 阿里巴巴德鲁伊druid连接池，开源免费

```java
import java.io.InputStream;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.Properties;

import javax.sql.DataSource;

import com.alibaba.druid.pool.DruidDataSourceFactory;

import net.nihao.day17.JDBCUtils;

public class Test {
	public static void main(String[] args) throws Exception{
		Properties properties = new Properties();
		InputStream is = Test.class.getClassLoader().getResourceAsStream("druid.properties");
		properties.load(is);
		
		
		// 创建druid连接池对象
		DataSource dataSource = DruidDataSourceFactory.createDataSource(properties);
		Connection connection = dataSource.getConnection();
		
		String sql = "select * from user where id = ?";
		PreparedStatement statement = connection.prepareStatement(sql);
		statement.setInt(1, 2);
		ResultSet rs = statement.executeQuery();
		
		while (rs.next()) {
			System.out.println(rs.getInt("id"));
			System.out.println(rs.getString("name"));
		}
		
		JDBCUtils.release(rs, statement, null);
	}

}
```

## 3、DBUtils

对JDBC进行简单封装的工具类库，开源免费的工具类库，使用它能够简化JDBC应用程序的开发，不会影响程序的性能

### 3.1 总步骤

1. 拷贝jar包
2. 创建QueryRunner()对象 传入DataSource
3. 调用query(sql, resultSetHandler,params)方法

### 3.2 ResultSetHandler结果集

```java
ArrayHandler：返回查询结果中的一行数据
    
ArrayListHandler：每行数据都对应存放在一个Object[] 数组中,多行数据的多个Object[]数组存放在集合中
    
ScalarHandler()：封装单个记录的 eg:统计数量
    
BeanHandler(重要)：将查询结果的第一行存储到javaBean对象中

BeanListHandler(非常重要)：将查询到的所有结果扔进list里面
    
MapListHandler()：查询多条记录封装到List<Map> list
```

### 3.3 DBUtils的常用API

#### 3.3.1 update增删改

1. 创建QueryRunner对象，并提供连接池，DBUtils底层自动维护连接Connection

2. QueryRunner执行增删改

   ​		int update(String sql, Object...params)执行增删改的sql语句

```java
import org.apache.commons.dbutils.QueryRunner;
import net.wanhe.day20.第三方连接池.C3P0Utils;

public class Test {
	public static void main(String[] args) throws Exception {
		// 1. 创建QueryRunner对象，传入连接池
		QueryRunner qr = new QueryRunner(C3P0Utils.getDataSource());
		
		//2.执行增删改
		String sql = "insert into user values(null, ?, ?)";
        int rows = qr.update(sql, "徐然", "12345678");
        System.out.println("增加操作受影响的行数：" + rows);
        
		String sql1 = "update user set password = ? where name = ?";
        int row1 = qr.update(sql1, "1234567", "小呆");
        System.out.println("修改操作受影响的行数：" + row1);
        
		String sql2 = "delete from user where name = ?";
		int row2 = qr.update(sql2, "root");
		System.out.println("删除操作受影响的行数：" + row2);
	}
}
```

#### 3.3.2 BeanHandler(T) 单行数据查询

```java
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;

import net.wanhe.day17.User;
/**
* BeanHandler(重要)
* 	 将查询结果的第一行存储到javaBean对象中
* @throws Exception 
* */
public class Test2 {
	public static void main(String[] args) throws Exception {
		// 1.创建QueryRunner对象，传入连接池
		QueryRunner qr = new QueryRunner(C3P0Utils.getDataSource());
        
		// 2.编写sql语句
		String sql = "select * from user where id = ?";
        
        // 3.调用query方法执行SQL,BeanHandler的构造方法中传入javaBean类的Class对象
		User user = qr.query(sql, new BeanHandler<User>(User.class), 5);
        
        // 打印数据
		System.out.println(user);
        
        // 
	}

}
```

#### 3.3.3 ArrayListHandler() 单列数据查询

```java
import java.util.Arrays;
import java.util.List;

import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.ArrayListHandler;

/**
* ArrayListHandler
* 	每行数据都对应存放在一个Object[] 数组中,多行数据的多个Object[]数组存放在集合中 
* @throws Exception 
**/
public class Test2 {
	public static void main(String[] args) throws Exception {
		// 1.创建QueryRunner对象，构造方法中传递DataSource实现类对象
		QueryRunner qr = new QueryRunner(C3P0Utils.getDataSource());
        
		// 2.编写SQL语句
		String sql = "select name from user";
        
        // 3.qr调用query方法执行SQL
		List<Object[]> lists = qr.query(sql, new ArrayListHandler());
        
        // 4.遍历集合打印数据
		for (Object[] list : lists) {
			System.out.println(Arrays.toString(list));
		}
	}

}
```

#### 3.3.4 ArrayHandler() 单行数据查询

```java
import java.util.Arrays;

import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.ArrayHandler;

/**
* ArrayHandler 返回查询结果中的一行数据
**/
public class Test2 {
	public static void main(String[] args) throws Exception {
		// 1.创建QueryRunner对象，构造方法中传递DataSource实现类对象
		QueryRunner qr = new QueryRunner(C3P0Utils.getDataSource());
        
		// 2. 编写SQL语句
		String sql = "select * from user";
        
        // 3.调用query方法,返回结果的一行数据
		Object[] list = qr.query(sql, new ArrayHandler());
		System.out.println(Arrays.toString(list));
	}

}
结果是表中的第一行数据打印
 [1, 李阳, 12345]
```

#### 3.3.5 BeanListHandler 查询所有结果

```java
import java.util.List;

import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanListHandler;

import net.wanhe.day17.User;

/**BeanListHandler(非常重要)
 *    将查询到的所有结果扔进list里面
**/
public class Test2 {
	public static void main(String[] args) throws Exception {
		//创建QueryRunner对象，传入连接池
		QueryRunner qr = new QueryRunner(C3P0Utils.getDataSource());
		// 3. 调用方法，执行查询功能
		String sql = "select * from user";
		List<User> list = qr.query(sql, new BeanListHandler<User>(User.class));
		for (User emp : list) {
			System.out.println(emp);
		}
		
	}

}
```

#### 3.3.6 ScalarHandler 单个查询（函数）

```sql
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.ScalarHandler;

/* ScalarHandler(重要)
 * 	 适合单个查询,一个select查询的结果只有一个值
 */
public class Test2 {
	public static void main(String[] args) throws Exception {
		//创建QueryRunner对象，传入连接池
		QueryRunner qr = new QueryRunner(C3P0Utils.getDataSource());
		// 3. 调用方法，执行查询功能
		String sql = "select count(*) as '编号' from user";
		Object list = qr.query(sql, new ScalarHandler());
		System.out.println(list);
		
	}
}
```

#### 3.3.7 MapListHandler 查询所有数据

```java
import java.util.List;
import java.util.Map;

import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.MapListHandler;

// MapListHandler
// 将查询出的每一行数据存储到map集合中,再将每一个map集合存储list集合中
public class Test2 {
	public static void main(String[] args) throws Exception {
		//创建QueryRunner对象，传入连接池
		QueryRunner qr = new QueryRunner(C3P0Utils.getDataSource());
		// 3. 调用方法，执行查询功能
		String sql = "select * from user";
		List<Map<String,Object>> list = qr.query(sql, new MapListHandler());
        
        // 先遍历list,再遍历map
		for (Map<String, Object> map : list) {
			for (Object key : map.keySet()) {
				System.out.println(key + "\t" + map.get(key));
			}
		}
		System.out.println(list);	
	}

}
```

## 4、三层架构

通常意义上三层架构就是将整个业务划分为：

1. 界面层（JSP）：位于最上层，用于显示数据和接受用户输入的数据，为用户提供一种交互和操作的界面
2. 业务层（逻辑层 service）
3. 持久层（数据访问层）：功能：负责数据库的访问

![](https://github.com/lixingyi123/JavaNotes/blob/main/java-basics/15-jdbc-%E8%BF%9E%E6%8E%A5%E6%B1%A0/images/%E4%B8%89%E5%B1%82%E6%9E%B6%E6%9E%84.png?raw=true)

