# 1. 初识MyBatis

## 1.1 MyBatis配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
  <mappers>
    <mapper resource="org/mybatis/example/BlogMapper.xml"/>
  </mappers>
</configuration>
```

## 1.2 Mapper配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
```

## 1.3 构建代码

```java
String resource = "org/mybatis/example/mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
```

## 1.4 MyBatis初始DataSource

​	Environment为DaTaSource初始化内容。配置好之后，由SqlSessionFactoryBuild根据获取的数据初始化DataSource。

## 1.5 MyBatis建Imp

​	1.1 中的mappers为1.2 中的配置文件，MyBatis由1.1 找到1.2 ，并根据1.2 内容构建DAO层的实现类。

## 1.6 MyBatis.xml 的mappers.xml 配置方式

### 16.1 resource 配置

- resource 方式：
  - 通过目录的方式找到Mapper的配置文件。

- class 方式：
- url 方式：

## 1.7 mapper.xml中类的配置

### 1.7.1 namespace配置

namespace 为实现类的接口，该xml为实现该类的实现过程。

### 1.7.2 SQL语句

- id：
  - SQL语句中的ID，与之对应的为需要实现接口的方法名。
- 传入参数类型
  - parameterType
    - MyBatis会为常用类、基本类型设置别名。
  - paramMap
- 返回值类型
  - resultType
  - resultSets
  - resultMap

# 2. MyBatis配置

## 2.1 引入外部配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <properties resource="db.properties">
        <property name="kkk" value="aaaa"/>
    </properties>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="com/acompe/mapper/UserMapper.xml"/>
    </mappers>
</configuration>
```

- 此处引入properties属性
  - 通过resource指向所引文件位置
  - 同时可以通过property属性在该元素中给properties文件新添加内容。
  - 当properties属性与文件属性重名，文件优先级较高。

## 2.2 给类起别名

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <properties resource="db.properties">
        <property name="kkk" value="aaaa"/>
    </properties>

    <typeAliases>
        <typeAlias type="com.acompe.pojo.entity.User" alias="User"/>
        <package name="com.acompe.pojo"/>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="com/acompe/mapper/UserMapper.xml"/>
    </mappers>
</configuration>
```

- typeAlias 同过指定类的方式给类起别名
  - alias为别名的名称，起别名后，文件其余配置均可使用别名。

- package 通过指定包给包中的类起别名
  - 别名为类名称，MyBatis建议别名类名称首字母小写。
- @Alias("别名") 可以通过注解方式，给类加上别名。

## 2.3 给MyBatis设置

- cacheEnable
  - 缓存是否开启
- lazyLoadingEnabled
  - 懒加载是否开启
- useGenerateKeys
  - 自动生成主键值
- mapUnderscoreToCamelCase
  - 将数据库_方式与Java驼峰方式进行自动转换

## 2.4 mapper映射器

```xml
<mappers>
  <mapper resource="com/acompe/mapper/UserMapper.xml"/>
  <mapper class="com.acompe.mapper.UserMapper"/>
  <mapper url="网络路径"/>
  <package name="com.acompe.mapper"/>
</mappers>
```

- resources
  - 通过本地资源路径进行加载
-  url
  - 通过网络资源路径进行加载
- class
  - 通过注释，加载类的方式进行加载
  - 通过XML
    - XML与class同一包下
    - XML与class同名
- package
  - 通过给出包名，自动遍历加载的方式进行加载
    - XML与class同一包下
    - 名称一样

# 3. Mapper配置

## 3.1 数据库与实体属性名不一致

- 传出时不一致

  - 通过给SQL起别名的方式，将其保证一直。

  - ResultMap 结果集映射

    ```xml
    <resultMap id="UserMap" type="User">
      <result column="pwd" property="password"/>
    </resultMap>
    
    <select id="findAll" resultMap="UserMap">
      select * from user;
    </select>
    ```

    - ResultMap 为结果集映射
    - result 为映射的一个内容
    - column 为数据库的列名称
    - property 为实体类属性名

- 传入时不一致

  - 基于配置文件
    - map传入
    - paramMap传入

  - 基于注解

    - 使用@Param("")
      - 单值时不需要用（建议除引用类型外均加上）
      - 引用类型不需要用

    ```java
    @Select("select * from user where id = #{id}")
    User findUserById(@Param("id") Long id);
    ```

- 注意
  - \#{} MyBatis会采用PreparStetment进行预编译
  - \${} MyBatis会采用拼接方式，不安全。

# 3. 复杂查询

## 3.1 多对一

- 嵌套查询

```xml
<resultMap id="StudentTeacher" type="Student">
  <result property="id" colum="id"/>
  <result property="name" colum="name"/>
  <association property="teacher" colum="tid" javaType="Teacher" select="getTeacher"/>
</resultMap>

<select id="getStudent" resultMap="StudentTeacher">
  select * from student
</select>

<select id="getTeacher" resultMap="Teacher">
	select * from teacher where id = #{}
</select>
```

- 直接查询

```xml
<resultMap id="StudentTeacher" type="Student">
  <result property="id" colum="sid"/>
  <result property="name" colum="sname"/>
  <association property="teacher" javaType="Teacher">
  	<result property="name" colum="tname"/>
  </association>
</resultMap>

<select id="getStudent" resultMap="StudentTeacher">
  select s.id sid, s.name sname,t.name tname
  from student s,teacher t
  where s.tid = t.id
</select>
```

## 3.2 一对多

- 嵌套查询

```xml
<select id="getStudentByTeacherId" resultType="Student">
  select * from student where tid = #{id}
</select>

<resultMap id="TeacherStudent" type="Teacher">
  <collection property="students" javaType="ArrayList" ofType="Student"  select="getStudentByTeacherId"/>
</resultMap>

<select id="getTeacher" resultMap="TeacherStudent">
	select * from teacher where id = #{id}
</select>
```



- 直接查询

```xml
<resultMap id="TeacherStudent" type="Teacher">
  <result property="id" column="tid"/>
  <result property="name" column="tname"/>
  <collection property="students" ofType="Student">
    <result property="id" column="sid"/>
  	<result property="name" column="sname"/>
    <result property="tid" column="tid"/>
  </collection>
</resultMap>

<select id="getStudent" resultMap="StudentTeacher">
  select s.id sid, s.name sname,t.name tname,t.id tid
  from student s,teacher t
  where s.tid = t.id
  and t.id = #{id}
</select>
```





