# Spring学习

# 1. IOC

## 1.1 基于配置文件

### 1.1.1 bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="accountDao" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
        <property name="accountDao" value="accountDao"/>
    </bean>
  
    <bean id="petStore" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
        <property name="accountDao" ref="accountDao"/>
    </bean>
</beans>
```

- 配置文件
  
  - beans
    
    - beans中可以包含多个bean
    
  - import
  
    - 可以导入其他的文件到当前文件
  
      ```xml
      <import resource="services.xml"/>
      ```
  
  - bean
  
    - 每一个bean都有一个Id，供外部获取用。
    - 每一个bean都有一个class，代表的那个类的bean，需要包名+别名。
    - 每一个bean都有一个name，代表的是那个类的别名，也可以用alias。
    - 每一个bean都有一个scope，默认为单利模式，也可以设置其他模式。
    - 每当类中有需要传入的属性，都需要一个property
  
  - property传入方式（set注入）
    - 使用name、value传入固定值
    - 通过ref方式，传入相应bean
  
  - constructor-arg 传入方式（构造器注入）
  
    - index 方式(使用ref 或value赋值)
  
      ```xml
      <bean id="index" class="examples.ExampleBean">
          <constructor-arg index="0" value="7500000"/>
          <constructor-arg index="1" ref="type"/>
      </bean>
      ```
  
    - type 方式(使用ref 或value赋值)
  
      ```xml
      <bean id="exampleBean" class="examples.ExampleBean">
          <constructor-arg type="int" value="7500000"/>
          <constructor-arg type="java.lang.String" ref="name"/>
      </bean>
      ```
  
    - name 方式(使用ref 或value赋值)
  
      ```xml
      <bean id="exampleBean" class="examples.ExampleBean">
          <constructor-arg name="userName" value="1000"/>
          <constructor-arg name="passWord" ref="index"/>
      </bean>
      ```
  
  - alias
  
    - 起别名后，别名相当于id
  
    - 别名与id同时可用
  
      ```xml
      <alias name="bean的id" alias="别名"/>
      ```
  

### 1.1.2 手动装配

##### 1.1.2.1 Set注入

- 普通注入

```xml
<bean id="student" class="com.acompe.pojo.entity.Student">
  <property name="name" value-"yanguoyu"/>
</bean>
```

- bean注入

```xml
<bean id="address" class="com.acompe.pojo.entity.Address">
  <property name="name" value="地址"/>
</bean>
<bean id="student" class="com.acompe.pojo.entity.Student">
  <property name="name" value="yanguoyu"/>
  <property name="address" value="address"/>
</bean>
```

- 数组注入

```xml
<bean id="student" class="com.acompe.pojo.entity.Student">
  <property name="book">
  	<array>
      <value>水浒传</value>
      <value>西游记</value>
    </array>
  </property>
</bean>
```

- List注入

```xml
<bean id="student" class="com.acompe.pojo.entity.Student">
  <property name="hobby">
  	<list>
    	<value>唱歌</value>
      <value>跳舞</value>
    </list>
  </property>
</bean>
```

- map注入

```xml
<bean id="student" class="com.acompe.pojo.entity.Student">
  <property name="cards">
    <map>
      <entry key="身份证" value="123"/>
      <entry key="银行卡" value="123"/>
    </map>
  </property>
</bean>
```

- set注入

```xml
<bean id="student" class="com.acompe.pojo.entity.Student">
  <property name="games">
  	<set>
    	<value>LOL</value>
      <value>DATA</value>
    </set>
  </property>
</bean>
```

- Null注入

```xml
<bean id="student" class="com.acompe.pojo.entity.Student">
  <property name="email">
  	<null/>
  </property>
</bean>
```

- properties注入

```xml
<bean id="student" class="com.acompe.pojo.entity.Student">
  <property name="info">
  	<props key="学号">123</props>
    <props key="专业">核能</props>
  </property>
</bean>
```

- p标签注入（set注入）

```xml
<bean id="student" class="com.acompe.pojo.entity.Student" p:name="yan" p:age="18"/>
```

##### 1.1.2.2 构造器注入

- c标签注入(构造器注入)

```xml
<bean id="student" class="com.acompe.pojo.entity.Student" c:name="yan" c:age="18"/>
```

### 1.1.3 自动装配

- byName(根据属性名与id自动装配)

```xml
<bean id="student" class="com.acompe.pojo.entity.Student" autowire="byName">
  <property name="name" value-"yanguoyu"/>
</bean>
```

- byType（根据类型自动装配,bean可以缺省id值）

```xml
<bean id="student" class="com.acompe.pojo.entity.Student" autowire="byType">
  <property name="name" value-"yanguoyu"/>
</bean>
```

## 1.2 基于注解

### 1.2.1 前提

- 导入约束
- 配置注解

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
		<!--开启注解-->
    <context:annotation-config/>
		<!--自动扫描以下包中带有@Componment注解的class类为bean-->
  	<context:component-scan base-package="com.acompe.pojo"/>
</beans>
```

### 1.2.2 bean

- @Configuration
  
- 该注解等价于<beans>
  
- 利用注解生成bean

  ```java
  @Component
  public class Person{
    private String name;
  }
  ```

  - Dao层
    - 采用@Repository注解生成bean
  - Service层
    - 采用@Service注解生成bean
  - Controller
    - 采用@Controller注解生成bean

- 利用注解注入

  ```java
  @Component
  public class Person{
    @Value("yanguoyu")
    private String name;
  }
  ```

  

- 利用注解设置scope

  ```java
  @Component
  @Scope("singleton")
  public class Person{
    @Value("yanguoyu")
    private String name;
  }
  ```

  

### 1.2.3装配

- 使用(使用byType自动装配、没有用byName)

```java
public class Person{
	@autowired
  //@Qualifier(value="id名") 当 cat 与 bean 中的id不一致，无法自动装配时，用来指定bean进行装配
  Cat cat;
  //@autowired
  public setCat(Cat cat){
    this.cat = cat;
  }
}
```

科普

```java
@Nullable  										 //参数可以为NULL
@autowired（required=false） 		//可以为空
@resource											 //java原生注解，自动装配
@resource(name="")						 //相当于autowired与qualifier(value="")结合使用
```

## 1.3 使用

- xml与annotation
  - bean推荐用xml来配置
  - 注入推荐用用注解来配置

```java
ApplicationContext context = new ClassPathApplicationContext("beans.xml");
//Student student = (Student)context.getBean("student");
Student student = context.getBean("student",Student.class);
```

# 2. AOP

## 2.1 相关概念

- 横切关注点
- 切面（ASPECT）
- 通知（Advice）
- 目标（Target）
- 代理（Proxy）
- 切入点（PointCut）
- 连接点（JoinPoint）

## 2.2 配置方式实现

### 2.2.1 方式一

```xml
<bean id="userService" class="com.acompe.service.userService"/>
<bean id="logBefore" class="com.acompe.log.logBefore"/>
<bean id="logAfter" class="com.acompe.log.logAfter"/>
<aop:config>
	<aop:pointCut id="pointcut" expression="execution(* com.acompe.service.UserServiceImpl.*(..))"/>
  
  <aop:advisor advice-ref="logBefore" pointcut-ref="pointcut"/>
  <aop:advisor advice-ref="logAfter" pointcut-ref="pointcut"/>
</aop:config>
```

其中，切面应该implements 相关类，例如

```java
public class logBefore implements MethodBeforeAdvice{
  @override
	public void before(Method method,Object[] args,Object target){
    //相应要执行之前的代码
  }  
}
```

### 2.2.2 方式二

```xml
<bean id="diy" class="com.acompe.diy.diyPointCut"/>

<aop:config>
	<aop:aspect ref="diy" >
  	<aop:pointCut id="pointCut" expression="execution(* com.acompe.service.UserServiceImpl.*(..))"/>
    
    <aop:before method="before" pointcut-ref="pointcut"/>
    <aop:after method="after" pointcut-ref="pointcut"/>
  </aop:aspect>
</aop:config>
```

其中，切面可以自己定哦，方法必须在before、after等对应。

```java
public class diyPointCut{
  public void before(){
    //相应要执行之前的代码
  }
  public void after(){
    //相应要执行之前的代码
  }
}
```

## 2.3 注解方式

1. 标注切入类为切面

   ```java
   @Aspect
   public class AnnotationPointCut{
     @Before("execution(* com.acompe.service.UserServiceImpl.*(..))")
     public void before(){
       
     }
   }
   ```

2. 在配置文件中配置bean

   ```xml
   <bean id="annotationPointCut" class="com.acompe.diy.AnnotationPointCut" />
   ```

3. 在配置文件中开启自动切入

   ```xml
   <aop:aspectj-autoproxy/>
   ```

   

# 3. 事务

```xml
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
  <property name="dataSource" ref="dataSource"
</bean>

  <!--通过该配置确定用aop方式以何种规则写入事务-->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
	<tx:attributes>
  	<tx:method name="方法名称"/>
  </tx:attributes>
</tx:advice>
  
<aop:config>
	<aop:pointCut id="txPointCut" expression="execution(* com.acompe.service.UserServiceImpl.*(..))"/>
  
  <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
</aop:config>
```

