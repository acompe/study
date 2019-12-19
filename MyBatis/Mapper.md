## Mapper.xml
介绍：该文件配置了CRUD相关配置。

- 缓存
    - 介绍：以及缓存默认开启，二级缓存需要
    - 开启缓存
    ```xml
    <cache/>
    ```
    - 缓存设置
    ```xml
    <cache
      eviction="FIFO"
      flushInterval="60000"
      size="512"
      readOnly="true"/>
    ```

- 结果集映射
    - 介绍：将查询结果以指定形式封装成指定类。
    ```xml
    <resultMap id="userResultMap" type="User">
      <id property="id" column="user_id" />
      <result property="username" column="user_name"/>
      <result property="password" column="hashed_password"/>
    </resultMap>
    ```
    - 一对多映射
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
        	select * from teacher where id = #{tid}
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
    - 多对一映射
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
      
- 引用SQL
    - 方式一
    ```xml
    <sql id="userColumns"> ${alias}.id,${alias}.username,${alias}.password </sql>
    
    <select id="selectUsers" resultType="map">
      select
        <include refid="userColumns"><property name="alias" value="t1"/></include>,
        <include refid="userColumns"><property name="alias" value="t2"/></include>
      from some_table t1
        cross join some_table t2
    </select>
    ```
    - 方式二
    ```xml
    <sql id="sometable">
      ${prefix}Table
    </sql>
    
    <sql id="someinclude">
      from
        <include refid="${include_target}"/>
    </sql>
    
    <select id="select" resultType="map">
      select
        field1, field2, field3
      <include refid="someinclude">
        <property name="prefix" value="Some"/>
        <property name="include_target" value="sometable"/>
      </include>
    </select>
    ```
- select
```xml
<select
  id="selectPerson"
  parameterType="int"
  parameterMap="deprecated"
  resultType="hashmap"
  resultMap="personResultMap"
  flushCache="false"
  useCache="true"
  timeout="10"
  fetchSize="256"
  statementType="PREPARED"
  resultSetType="FORWARD_ONLY">
```
```xml
<select id="selectPerson" parameterType="int" resultType="hashmap">
  SELECT * FROM PERSON WHERE ID = #{id}
</select>
```

- insert
```xml
<insert
  id="insertAuthor"
  parameterType="domain.blog.Author"
  flushCache="true"
  statementType="PREPARED"
  keyProperty=""
  keyColumn=""
  useGeneratedKeys=""
  timeout="20">
```
```xml
<insert id="insertAuthor">
  insert into Author (id,username,password,email,bio)
  values (#{id},#{username},#{password},#{email},#{bio})
</insert>
```
- update
```xml
<update
  id="updateAuthor"
  parameterType="domain.blog.Author"
  flushCache="true"
  statementType="PREPARED"
  timeout="20">
```
```xml
<update id="updateAuthor">
  update Author set
    username = #{username},
    password = #{password},
    email = #{email},
    bio = #{bio}
  where id = #{id}
</update>
```
- delete
```xml
<delete
  id="deleteAuthor"
  parameterType="domain.blog.Author"
  flushCache="true"
  statementType="PREPARED"
  timeout="20">
```
```xml
<delete id="deleteAuthor">
  delete from Author where id = #{id}
</delete>
```
以上解释官网均有解释