#IOC
## 相关概念
- IOC ：控制反转,将类的对象的创建交给Spring类管理创建。
- DI：依赖注入,将类里面的属性在创建类的过程中给属性赋值。
- IOC与DI关系：DI和IOC的关系: DI不能单独存在,DI需要在IOC的基础上来完成。
## 配置文件实现
- beans
    - 相当于IOC，beans中的bean为Spring需要管理创建的类。
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
- import
    - 一般用于将大的xml文件分功能拆解
    - 当有多个配置文件时，通过import将多个xml文件融合为一个文件。
    ```xml
      <import resource="services.xml"/>
    ```
- bean
    - 对交由Spring创建的类进行配置。
    - id
        - 每一个bean的唯一识别
    - name
        - 别名，相当于另外的id，可以用逗号、分号、|线分割多个别名。
    - class
        - 类，指定哪个类交由Spring创建管理。
    - scope
        - 作用域，指明实力的作用域，单例、多例等。
    ```xml
      <bean id="accountDao" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
          <property name="accountDao" value="accountDao"/>
      </bean>
    ```
- constructor-arg
    - 相当于DI注入，以构造器的方式注入内容到实例。
    - 指定注入位置
        - index：通过第几个位置指定
        - type：通过指定类型，自动寻找注入
        - name：通过指定参数名称，自动寻找注入
    ```xml
      <bean id="index" class="examples.ExampleBean">
          <constructor-arg index="0" value="7500000"/>
          <constructor-arg index="1" ref="type"/>
      </bean>
    ```
- property
    - 相当与DI注入，以Set函数的方式注入的内容实例。
    - name
        - 类中需要注入的参数
    - value
        - 类中参数需要注入的值
    ```xml
    <bean id="accountDao" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
      <property name="accountDao" value="accountDao"/>
    </bean>
    ```
- value、ref
    - value
        - 通过直接赋值的方式注入
    ```xml
      <constructor-arg index="0" value="7500000"/>
    ```
    - ref
        - 通过将其他bean以引用的方式注入
    ```xml
      <constructor-arg index="1" ref="type"/>
    ```
- alias
    - 起别名，相当于bean中的name
    ```xml
      <alias name="bean的id" alias="别名"/>
    ```
- 注入方式
    - 手动注入
        - 普通注入
        ```xml
          <bean id="student" class="com.acompe.pojo.entity.Student">
            <property name="name" value-"yanguoyu"/>
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
        - c标签注入(构造器注入)
        ```xml
          <bean id="student" class="com.acompe.pojo.entity.Student" c:name="yan" c:age="18"/>
        ```
    - 自动注入
        - byName(根据属性名与id自动装配)
        ```xml
          <bean id="student" class="com.acompe.pojo.entity.Student" autowire="byName">
          </bean>
        ```
        - byType（根据类型自动装配,bean可以缺省id值）
        ```xml
          <bean id="student" class="com.acompe.pojo.entity.Student" autowire="byType">
          </bean>
        ```
## 注解实现
- 前提
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
- beans注解
    - @Configuration
- bean注解
    - @bean：该注解为函数注解，要求返回一个实例
    - @Component：该注解为类注解，注释后由Spring创建一个实例
    ```java
      @Component
      public class Person{
        private String name;
      }
    ```
    - @Repository
        - 在Dao中的Component注解
    - @Service
        - 在Service层的Component注解
    - @Controller
        - 在Controller层的Component注解
- value
    - 实例注解注入
    ```java
      @Component
      public class Person{
        @Value("yanguoyu")
        private String name;
      }
    ```
- scope
    - 注解实现作用域
    ```java
      @Component
      @Scope("singleton")
      public class Person{
        @Value("yanguoyu")
        private String name;
      }
    ```
- autowired
    - 注解实现自动装配
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
- 其他注释
```xml
@Nullable  										 //参数可以为NULL
@autowired（required=false） 		             //可以为空
@resource									     //java原生注解，自动装配
@resource(name="")						         //相当于autowired与qualifier(value="")结合使用
```
## 使用方法
- xml与annotation
    - bean推荐用xml来配置
    - 注入推荐用用注解来配置
    
```java
ApplicationContext context = new ClassPathApplicationContext("beans.xml");
//Student student = (Student)context.getBean("student");
Student student = context.getBean("student",Student.class);
```
