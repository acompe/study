# Maven 学习
## 1.获取
- 可以通过[Maven官网](https://maven.apache.org/download.cgi)直接进行下载。
## 2.文件目录
- bin
    - 该层为Maven的运行启动目录。
- lib
    - 该层为Maven的运行环境目录。
- conf
    - 该层为Maven的配置文件目录。
- 注意事项：
    - 运行Maven的时候需要环境边领JAVA_HOME
    - 运行Maven的时候最好配置MAVEN_HOME
    - 通过MAVEN_HOME配置快捷mvn。
## 3.配置文件
- 程序运行的时候会自动寻找conf中的setting，加载其配置。
- idea等IDE可以手动设置setting文件位置，与repository仓库位置。
- setting
  - 设置repository位置。
  - 设置中心仓库地址。
  - 设置中心仓库登陆账号、密码。
## 4.Maven项目结构
介绍：通过Maven创建的文件，默认都遵从Maven推荐的目录结构，利用Idea等IDE创建Maven项目的时候也都会遵循该目录结构。  
- src
    - main
        - java：java核心代码
        - resources：资源文件
        - webapp：网站html、jsp、css、js、图片等路径。
    - test
        - java：测试代码
        - resources：测试资源文件
## 5. mvn启动参数
- -DarchetypeCatalog=internal
    - 创建项目的时候不进行联网，使用本地仓库。
    - 在Idea中使用时，在maven配置项runner中配置该参数在启动时。
        - 将此参数传入，创建项目时比较快。
## 6. scope作用域
- 作用域表  

|---|编译|测试|运行|打包|
|:---:|:---:|:---:|:---:|:---:|
|compile(默认)|√|√|√|√|
|test|√|√|-|-|
|runntime|-|√|√|√|
|provided|√|√|√|-|
|system|√|√|√|-|
- 继承表，有nexus提供。

|-|compile|provided|runtime|test|
|:---:|:---:|:---:|:---:|:---:|
|compile|compile(*)|-|runtime|-|
|provided|provided|-|provided|-|
|runtime|runtime|-|runtime|-|
|test|test|-|test|-|
- 注意
    - system与privided相差不大，只是依赖文件会从本地文件系统中获取，需要与systemPath属性使用。
## 7.插件
- 插件引入
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
                <port>80</port>
                <path>/</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```
## 8.Idea对Maven支持
- 骨架支持
    - quickstart
        - java基本骨架
    - webapp
        - 网站基本骨架
- 模版支持
    - Live Template
        - 可以快速定义模版并引入。