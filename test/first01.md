#Hibernate入门

![Alt text](./0BTOLPVTEQN$2EO~MY~YK.png)

************************************************************************************************

![Alt text](./@~KH03B1]_M$@PX1BZ~0QP.png)

![Alt text](./W@8H4Z@$@FBXOO{JS11ON.png)
![Alt text](./ZYCQ7J{~}DREVENC4GB3.png)
![Alt text](./DP[{$[JE_EW}_@V8JYYSQL.png)
![Alt text](./O$5C4ICV~E0@FG3Q27ZN72.png)
![Alt text](./2XAAWEN${L}BVW[IOGY[DD.png)
![Alt text](./O6}HAC5S8J_BA]6XJRDWW.png)
![Alt text](./`QT{[@AP2Y_[}R{5P[LG7K5.png)

#以上是Hibernate的思维导图

ORM：对象关系映射

那么对象就是我们的javaBean了，就是一个对象跟数据库里的表相对应，操作对象就可以操作表。

####那么我们先来创建一个Customer对象和数据库中的表相对应

/*CREATE TABLE `cst_customer` (
		  `cust_id` BIGINT(32) NOT NULL AUTO_INCREMENT COMMENT '客户编号(主键)',
		  `cust_name` VARCHAR(32) NOT NULL COMMENT '客户名称(公司名称)',
		  `cust_source` VARCHAR(32) DEFAULT NULL COMMENT '客户信息来源',
		  `cust_industry` VARCHAR(32) DEFAULT NULL COMMENT '客户所属行业',
		  `cust_level` VARCHAR(32) DEFAULT NULL COMMENT '客户级别',
		  `cust_phone` VARCHAR(64) DEFAULT NULL COMMENT '固定电话',
		  `cust_mobile` VARCHAR(16) DEFAULT NULL COMMENT '移动电话',
		  PRIMARY KEY (`cust_id`)
		) ENGINE=INNODB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
*/
```
package cn.ly.hibernate.demo01;
public class Customer {
	private long cust_id;
	private String cust_name;
	private String cust_source;
	@Override
	public String toString() {
		return "Customer [cust_id=" + cust_id + ", cust_name=" + cust_name + ", cust_source=" + cust_source
				+ ", cust_industry=" + cust_industry + ", cust_level=" + cust_level + ", cust_phone=" + cust_phone
				+ ", cust_mobile=" + cust_mobile + "]";
	}
	private String cust_industry;
	private String cust_level;
	private String cust_phone;
	private String cust_mobile;
	public long getCust_id() {
		return cust_id;
	}
	public void setCust_id(long cust_id) {
		this.cust_id = cust_id;
	}
	public String getCust_name() {
		return cust_name;
	}
	public void setCust_name(String cust_name) {
		this.cust_name = cust_name;
	}
	public String getCust_source() {
		return cust_source;
	}
	public void setCust_source(String cust_source) {
		this.cust_source = cust_source;
	}
	public String getCust_industry() {
		return cust_industry;
	}
	public void setCust_industry(String cust_industry) {
		this.cust_industry = cust_industry;
	}
	public String getCust_level() {
		return cust_level;
	}
	public void setCust_level(String cust_level) {
		this.cust_level = cust_level;
	}
	public String getCust_phone() {
		return cust_phone;
	}
	public void setCust_phone(String cust_phone) {
		this.cust_phone = cust_phone;
	}
	public String getCust_mobile() {
		return cust_mobile;
	}
	public void setCust_mobile(String cust_mobile) {
		this.cust_mobile = cust_mobile;
	}
	
}
```

###下面就是我们今天的重要内容了。
	Customer.hbm.xml 的配置文件
	hibernate.cfg.xml 的配置文件

####我们先看看第一个Customer.hbm.xml

```
	<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
  <hibernate-mapping>
  	<!-- 建立类与表的映射 -->
  	  		<!-- 类名和表明一致 table可以省略 -->
  	<class name="cn.ly.hibernate.demo01.Customer" table="cst_customer">
  		<!-- 建立类中的属性与表中的主键对应 -->
  		<id name="cust_id" column="cust_id">
  			<!-- 主键生成策略（本地） -->
  			<generator class="native"/>
  		</id>
  		<!-- 类中的普通属性与表的字段的对应  type:java中的类型 不为空 而且 不唯一-->
  		<!-- 属性名和表明一致 column可以省略 -->
  		<property name="cust_name" column="cust_name" length="32" type="java.lang.String" not-null="true" unique="false"/>
  		<!-- type：Hibernate中的类型string -->
  		<property name="cust_source" column="cust_source" length="32" type="string"/>
  		<!-- type:数据库中的类型 -->
  		<property name="cust_industry"  length="32">
  			<column name="cust_industry" sql-type="varchar"></column>
  		</property>
  		<property name="cust_level" column="cust_level" length="32"/>
  		<property name="cust_phone" column="cust_phone" length="32"/>
  		<property name="cust_mobile" column="cust_mobile" length="32"/>
  	</class>
  </hibernate-mapping>    
	
```

其中dtd约束我们可以在
![Alt text](./GCN@WEJFVK0@[1~85W16R7.png)
在这个包下找到：
![Alt text](./1544346987034.png)
打开后就会发现
![Alt text](./1544347037890.png)

然后同样的路径下找到
![Alt text](./1544347071547.png)
里面就是：hibernate.cfg.xml的dtd约束了

Customer.hbm.xml里面主要是一个映射关系，也称为映射文件

###下面在看看另一个xml文件hibernate.cfg.xml


```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
  
<hibernate-configuration>
	<session-factory>
		<property name="hibernate.connection.driver_class">com.mysql.jdbc.Driver</property>
		<!-- <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/hibernate_day01</property> 因为是本机，所以可以省略localhost：3306 hibernate—day01是数据库名-->
		<property name="hibernate.connection.url">jdbc:mysql:///hibernate_day01</property>
		<property name="hibernate.connection.username">root</property>
		<property name="hibernate.connection.password">123456</property>
		<!-- 配置Hibernate的方言 -->
		<property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
		
		
		
		
		<!-- 可选配置 ===================-->
		
		<!-- 打印sql语句 -->   
		<property name="hibernate.show_sql">true</property>
		<!-- 格式化sql 打印的更好看 -->
		<property name="hibernate.format_sql">true</property>
		<!-- 自动建表 -->
		<!-- 
			none:不使用hibernate的自动建表
			create:如果已经有表，删除原有表，重新建表。如果没有表，新建表（测试）
			create-drop:有，删除，新建，执行操作，删除。  么有，新建，操作，删除。（测试）
			update:如果数据库中有表，使用原有表，如果没有表，创建新表（更新表结构）比如你在有表的情况下将配置文件中的column更改了。它就是自己加上一列
			validate:如果没有表，不会创建表。只会使用数据库中原有的表。（校验映射和表结构）
		 -->
		<property name="hibernate.hbm2ddl.auto">update</property>
		
		<!-- 配置C3P0连接池 （可以自己配置连接池，也可以不配置）-->
		<property name="connection.provider_class">org.hibernate.connection.C3P0ConnectionProvider</property>
		<!--在连接池中可用的数据库连接的最少数目 -->
		<property name="c3p0.min_size">5</property>
		<!--在连接池中所有数据库连接的最大数目  -->
		<property name="c3p0.max_size">20</property>
		<!--设定数据库连接的过期时间,以秒为单位,
		如果连接池中的某个数据库连接处于空闲状态的时间超过了timeout时间,就会从连接池中清除 -->
		<property name="c3p0.timeout">120</property>
		 <!--每3000秒检查所有连接池中的空闲连接 以秒为单位-->
		<property name="c3p0.idle_test_period">3000</property>
		<!-- 可选配置 ===================-->
		
		
		<!-- 引入映射文件（加载哪个映射，就是我们第一个xml文件啦） -->
		<mapping resource="cn/ly/hibernate/demo01/Customer.hbm.xml"/>
	</session-factory>
</hibernate-configuration>
```

因为里面出现了许多不认识的配置，我来带大家找一下吧（依次打开之后就可以看到了）
![Alt text](./1544347479401.png)
![Alt text](./1544347489202.png)
![Alt text](./1544347501245.png)

也可以引入log4j日志文件（可选项）

```
#
# Hibernate, Relational Persistence for Idiomatic Java
#
# License: GNU Lesser General Public License (LGPL), version 2.1 or later.
# See the lgpl.txt file in the root directory or <http://www.gnu.org/licenses/lgpl-2.1.html>.
#

### direct log messages to stdout ###
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

### direct messages to file hibernate.log ###
#log4j.appender.file=org.apache.log4j.FileAppender
#log4j.appender.file.File=hibernate.log
#log4j.appender.file.layout=org.apache.log4j.PatternLayout
#log4j.appender.file.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

### set log levels - for more verbose logging change 'info' to 'debug' ###
#（此处为注释）在控制台输出（当然也可以输出到日志文件里面）
log4j.rootLogger=info, stdout

#log4j.logger.cn.itcast.hibernate.log4j=trace

#log4j.logger.org.hibernate=info
#log4j.logger.org.hibernate=debug

### log HQL query parser activity
#log4j.logger.org.hibernate.hql.ast.AST=debug

### log just the SQL
#log4j.logger.org.hibernate.SQL=debug

### log JDBC bind parameters ###
#log4j.logger.org.hibernate.type=TRACE
#log4j.logger.org.hibernate.type=debug

### log schema export/update ###
#log4j.logger.org.hibernate.tool.hbm2ddl=debug

### log HQL parse trees
#log4j.logger.org.hibernate.hql=debug

### log cache activity ###
#log4j.logger.org.hibernate.cache=debug

### log transaction activity
#log4j.logger.org.hibernate.transaction=debug

### log JDBC resource acquisition
#log4j.logger.org.hibernate.jdbc=debug

### enable the following line if you want to track down connection ###
### leakages when using DriverManagerConnectionProvider ###
#log4j.logger.org.hibernate.connection.DriverManagerConnectionProvider=trace
```

#Hibernate的API

###Configuration 对象
```
//1.加载核心配置文件 也可以加载映射文件(当配置文件是hibernate.cfg.xml时)
		Configuration configuration = new Configuration().configure();
		//当配置文件是hibernate.properties时
//		Configuration configuration2 = new Configuration();
		//手动加载映射文件（这个一般在都在xml中配置了就不用手动加载了）
//		configuration.addResource("cn/ly/hibernate/demo01/Customer.hbm.xml");
```
###SessionFactory对象（重量级对象，加载比较慢）

SessionFactory：Session工厂
			---内部维护了Hibernate的连接池
				和二级缓存，是线程安全的对象。一个项目创建一个对象即可。
```
//2.创建一个SessionFactory对象：类似于JDBC中的连接池
		SessionFactory sessionFactory = configuration.buildSessionFactory();
		//3.SessionFactory获取到Session对象：类似于JDBC中的Connection
		Session session = sessionFactory.openSession();
```
因为是一个项目创建一个，所以我们可以将它抽象出来

```
package cn.ly.hibernate.utils;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

/**
 * Hibernate工具类
 * 
 * */

public class HibernateUtils {
	//一个项目创建一个对象即可。所以就抽象出了工具类
	public static final Configuration cfg;
	public static final SessionFactory sf;
	
	static {
		cfg = new Configuration().configure();
		sf = cfg.buildSessionFactory();
	}
	
	public static Session openSession() {
		return sf.openSession();
	}
	
}
```


###Session对象

```
Session代表的是Hibernate与数据库的连接对象，不是线程安全的，与数据库交互桥梁（里面可以执行SQL语句。。。等）
session.save(customer);//增
session.load(Customer.class, 8l);//查
session.get(Customer.class, 9l);//查
session.delete(customer2);//删
session.update(customer);//改
session.saveOrUpdate(customer2);//增或改
session.createQuery("from Customer");
session.createSQLQuery("select * from cst_customer");
session.close();
```

#下面就是具体session的增删该查的例子了
###（注意get和load的区别）

```
package cn.ly.hibernate.demo01;

import java.util.Arrays;
import java.util.List;

import org.hibernate.Query;
import org.hibernate.SQLQuery;
import org.hibernate.Session;
import org.hibernate.Transaction;
import org.junit.Test;

import cn.ly.hibernate.utils.HibernateUtils;

public class HibernateDemo02 {
	
	//插入记录
	//@Test  
	public void test() {
		/*
			Session代表的是Hibernate与数据库的连接对象，不是线程安全的，与数据库交互桥梁（里面有SQL语句。。。等）
			
		*/
		Session session = HibernateUtils.openSession();
		//开启事物
		Transaction transaction = session.beginTransaction();
		
		Customer customer = new Customer();
		customer.setCust_name("杨汉鹏");
		
		session.save(customer);
		//提交事物
		transaction.commit();
		//关闭连接
		session.close();
		
	}
	
	//查询
	/*
	 
	 get 和 load 都能查询，而且执行的语句一样，那他们有神魔区别呢？
	 
	 ***get采用的是立即加载,执行到这行代码的时候,就会马上发送SQL语句去查询
	 *	查询后返回的是真实对象本身
	 *   查询一个找不到的对象返回null
	 
	 ***load方法
	 *	采用的是延迟加载,(;lazy懒加载),执行这行代码的时候,不会发送SQL语句,当真正使用这个对象的时候才会发送SQL语句（使用id的时候也不会去发送SQL语句因为id是已知的）
	 *	查询后返回的是代理对象--->这个包javassist-3.18.1-GA.jar  动态代理：是实现接口的代理对象。但是这个没有实现接口，利用javassist技术产生的代理
	 *	查询找不到的对象时，返回ObjectNotFoundException
	 */
	//@Test
	public void test02() {
		Session session = HibernateUtils.openSession();
		Transaction transaction = session.beginTransaction();
		
//		Customer customer = session.get(Customer.class, 7l);
//		System.out.println(customer);
		Customer customer2 = session.load(Customer.class, 8l);
		System.out.println(customer2);
		
		transaction.commit();
		session.close();
		
	}
	
	//修改
	//@Test
	public void test03() {
		Session session = HibernateUtils.openSession();
		Transaction transaction = session.beginTransaction();
		//1.直接创建对象修改(相当于把原来的id为8的全部属性都改为了新创建的对象的属性了)
//		Customer customer = new Customer();
//		customer.setCust_id(8l);
//		customer.setCust_name("郭玉莹");
//		session.update(customer);
		
		//2.先查询在修改（推荐）
		Customer customer = session.get(Customer.class, 9l);
		customer.setCust_name("杨汉鹏");
		session.update(customer);
		
		
		
		transaction.commit();
		session.close();
		
	}
	
	//删除
	//@Test
	 public void test04() {
		Session session = HibernateUtils.openSession();
		Transaction transaction = session.beginTransaction();
		//1.创建对象删除
//		Customer customer = new Customer();
//		customer.setCust_id(10l);
//		session.delete(customer);
		//2.先查询再删除（推荐）---级联删除（比如有多表映射的关系，删除一个用户，用户下面的订单什么的也被删除了）
		Customer customer2 = session.get(Customer.class, 10l);
		session.delete(customer2);
		
		transaction.commit();
		session.close();
	}
	
	
	//@Test
	public void test05() {
		Session session = HibernateUtils.openSession();
		Transaction transaction = session.beginTransaction();
		//设置了一个名字，没有id为保存操作
//		Customer customer = new Customer();
//		customer.setCust_name("李四");
//		session.saveOrUpdate(customer);
		//设置了id为更新操作
		Customer customer2 = new Customer();
		customer2.setCust_id(1l);
		customer2.setCust_name("李四");
		session.saveOrUpdate(customer2);
		
		transaction.commit();
		session.close();
	}
	
	@Test
	//查询所有query对象都是由session创建的
	public void test06() {
		Session session = HibernateUtils.openSession();
		Transaction transaction = session.beginTransaction();
		
		//接收HQL:Hibernate Query Language面向对象的查询语言
		//"from Customer":Customer是一个类，而不是表名
		Query query = session.createQuery("from Customer");
		List<Customer> list = query.list();
		for(Customer customer:list) {
			System.out.println(customer);
		}
		
		//接收SQL
//		SQLQuery query = session.createSQLQuery("select * from cst_customer");
//		List<Object[]> list = query.list();
//		for(Object[] obj :list) {
//			System.out.println(Arrays.toString(obj));
//		}
//		
		transaction.commit();
		session.close();
		
	}
	
	
	
}
```



