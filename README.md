# InterviewSpringMvc

Before Spring (servlet and Context)
-------------
Method getServletContextName() returns the name of the "web application". 
That means, "ServletContext" is nothing but "web application". Ok.
A ServletContext is the runtime representation of the web application.
A ServletContextListener gets notified when a Web App is started or stopped. That way you can run tasks automatically that need to be run when the web app starts or stops.

applicationContext.xml defines the beans that are shared among all the servlets. If your application have more than one servlet, then defining the common resources in the applicationContext.xml would make more sense.

spring-servlet.xml defines the beans that are related only to that servlet. Here it is the dispatcher servlet. So, your Spring MVC controllers must be defined in this file.

There is nothing wrong in defining all the beans in the spring-servlet.xml if you are running only one servlet in your web application.



why sprig popular ?
dependeny injection or Inversion of Control, can use classes that you want just by autowiring
don't have to use the new keyword, but with some <xml> file or annotation based we can use the required class

eg: if any clientBusiness depends upon client and product classes
then in clientBusiness class we can just
call the dependent object as

@Service
public class ClientBOImpl implements ClientBO{
@AutoWired
clientDO client;

@AutoWired
ProdutDO product;
}


versions
-------
spring 2.5=annotation
spring 3.0= java 5 new (genrics)
spring 4= java 8 (latest) lambda.. min 6 is required, @RestController,  (servlet 3.0 is used)

AutoWiring
----------
auto finding of required bean depedencies
@service or @Component should be used in model

SingleTon Bean
-------------
only one instance of the bean is in JVM once (saving memory) is default is singleton

to make the bean stateful, for each request of this bean new instance of this bean in jvm is created by
using prototype
<bean id="state" class="com.foo.SomeState" scope="prototype">


AOP
---
Spring AOP (Aspect-oriented programming) framework is used to modularize cross-cutting concerns in aspects. Put it simple, it’s just an interceptor to intercept some processes, for example, when a method is execute, Spring AOP can hijack the executing method, and add extra functionality before or after the method execution.

In Spring AOP, 4 type of advices are supported :

Before advice – Run before the method execution
After returning advice – Run after the method returns a result
After throwing advice – Run after the method throws an exception
Around advice – Run around the method execution, combine all three advices above
Most of the Spring developers are just implements the ‘Around advice ‘, since it can apply all the advice type

WEB layers //forms
Business Layers //models and conditions
Database layers //dao layers
(logging,security,transactions all should be set in all above 3 layers they are AOP Aspect oriented programming concept)


Integrate spring and Hibernate
------------------------------
SessionFactory bean can be created configuring in xml file

<bean id="hibernate4AnnotatedSessionFactory"
		class="org.springframework.orm.hibernate4.LocalSessionFactoryBean">
		<property name="dataSource" ref="dataSource" />
		<property name="annotatedClasses">
			<list>
				<value>com.journaldev.model.Person</value>
			</list>
		</property>
		<property name="hibernateProperties">
			<props>
				<prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
				<prop key="hibernate.current_session_context_class">thread</prop>
				<prop key="hibernate.show_sql">false</prop>
			</props>
		</property>
	</bean>
	
	or can use jpa for hibernate  in application.properties
	
	# DataSource settings: set here your own configurations for the database 
# connection. In this example we have "netgloo_blog" as database name and 
# "root" as username and password.
spring.datasource.url = jdbc:mysql://localhost:8889/netgloo_blog
spring.datasource.username = root
spring.datasource.password = root

# Keep the connection alive if idle for a long time (needed in production)
spring.datasource.testWhileIdle = true
spring.datasource.validationQuery = SELECT 1

# Show or not log for each sql query
spring.jpa.show-sql = true

# Hibernate ddl auto (create, create-drop, update)
spring.jpa.hibernate.ddl-auto = update

# Naming strategy
spring.jpa.hibernate.naming-strategy = org.hibernate.cfg.ImprovedNamingStrategy

# Use spring.jpa.properties.* for Hibernate native properties (the prefix is
# stripped before adding them to the entity manager)

# The SQL dialect makes Hibernate generate better SQL for the chosen database
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5Dialect

JPA is the interface, its implementation is Hibernate


Spring Cahsing
--------------
Ehcache,Jcache

to enable cahsing we can use xml or annotation based config
1. first step enable cash to class
@EnableCaching
class Account
2. 2nd method enable cash to method
@cachable("withdraw")  // to cash methods you like 
public diwithdraw(Account ac, int bal){
}

SpringBatch
----------
to perform batch programming, good feature is it resumes from where it was stopped 
