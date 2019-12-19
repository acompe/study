## MyBatis-config.xml
介绍：该文件配置了MyBatis全局配置。
- 配置文件配置
    - 介绍：当该文件要引用外部配置文件时，需要使用该配置，该配置还可以在此处通过property配置其余属性，配置文件ID相同时，外部配置文件优先级较高。
```xml
<properties resource="org/mybatis/example/config.properties">
  <property name="username" value="dev_user"/>
  <property name="password" value="F2Fa3!33TYyg"/>
</properties>
```

- MyBatis配置
    - 介绍：该配置文件为开启MyBatis的某些功能时使用，具体参数作用来源于官方网站。
```xml
<settings>
  <setting name="cacheEnabled" value="true"/>
  <setting name="lazyLoadingEnabled" value="true"/>
  <setting name="multipleResultSetsEnabled" value="true"/>
  <setting name="useColumnLabel" value="true"/>
  <setting name="useGeneratedKeys" value="false"/>
  <setting name="autoMappingBehavior" value="PARTIAL"/>
  <setting name="autoMappingUnknownColumnBehavior" value="WARNING"/>
  <setting name="defaultExecutorType" value="SIMPLE"/>
  <setting name="defaultStatementTimeout" value="25"/>
  <setting name="defaultFetchSize" value="100"/>
  <setting name="safeRowBoundsEnabled" value="false"/>
  <setting name="mapUnderscoreToCamelCase" value="false"/>
  <setting name="localCacheScope" value="SESSION"/>
  <setting name="jdbcTypeForNull" value="OTHER"/>
  <setting name="lazyLoadTriggerMethods" value="equals,clone,hashCode,toString"/>
</settings>
```

- 别名配置
    - 介绍：该配置可以给指定类起别名，防止在配置文件中需要太多的包前缀，起别名共有如下几种方式。
    - 给指定类起别名
    ```xml
    <typeAliases>
      <typeAlias alias="Author" type="domain.blog.Author"/>
    </typeAliases>
    ```
    - 给指定范围类起别名
    ```xml
    <typeAliases>
      <package name="domain.blog"/>
    </typeAliases>
    ```
  
- 环境配置
    - 介绍：该配置为配置Config，其中包括数据源、事务类型。
```xml
<environments default="development">
  <environment id="development">
    <transactionManager type="JDBC">
      <property name="..." value="..."/>
    </transactionManager>
    <dataSource type="POOLED">
      <property name="driver" value="${driver}"/>
      <property name="url" value="${url}"/>
      <property name="username" value="${username}"/>
      <property name="password" value="${password}"/>
    </dataSource>
  </environment>
</environments>
```

- 映射器配置
    - 介绍：该配置为指定所有的映射器，只有指定的映射器，才能将接口与执行SQL连接起来CRUD，其中配置方式共以下四种。
    - 指定配置文件配置
    ```xml
    <mappers>
      <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
    </mappers>
    ```
    - 指定网络资源配置
    ```xml
    <mappers>
      <mapper url="file:///var/mappers/AuthorMapper.xml"/>
      <mapper url="file:///var/mappers/BlogMapper.xml"/>
      <mapper url="file:///var/mappers/PostMapper.xml"/>
    </mappers>
    ```
    - 指定配置类配置(该方式用于注解|配置文件名与类名相同，且在同一包内)
    ```xml
    <mappers>
      <mapper class="org.mybatis.builder.AuthorMapper"/>
      <mapper class="org.mybatis.builder.BlogMapper"/>
      <mapper class="org.mybatis.builder.PostMapper"/>
    </mappers>
    ```
    - 通过指定扫描路径(该方式用于注解|配置文件名与类名相同，且在同一包内)
    ```xml
    <mappers>
      <package name="org.mybatis.builder"/>
    </mappers>
    ```