# AOP
# 相关概念
- AOP为切面编程，可以将任何代码块看成分割的部分，在该代码块前后切入代码、事务等。
- 横切关注点
- 切面（ASPECT）
- 通知（Advice）
- 目标（Target）
- 代理（Proxy）
- 切入点（PointCut）
- 连接点（JoinPoint）
# 配置文件方式切入
- 官方方式切入
    - 编写配置文件
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
    - 编写切入的代码
    ```java
      public class logBefore implements MethodBeforeAdvice{
        @override
      	public void before(Method method,Object[] args,Object target){
          //相应要执行之前的代码
        }  
      }
    ```
- 自定义方式切入
    - 编写配置文件
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
    - 编写切入代码
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
# 注解方式切入
- 编写代码并写入注解
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
- 将此切面配置bean
```xml
<bean id="annotationPointCut" class="com.acompe.diy.AnnotationPointCut" />
```
- 开启注释切入
```xml
<aop:aspectj-autoproxy/>
```
# 事务
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