# mybatis-dalgen
自动生成mybatis配置文件及DAO部分代码

##使用方法
1、将本项目拷贝至工程根目录下
2、修改工程相关配置：system-config.properties
3、运行gen.bat文件

##
由于MyBatis属于一种半自动的ORM框架，所以主要的工作就是配置Mapping映射文件，但是由于手写映射文件很容易出错，所以可利用MyBatis生成器自动生成实体类、DAO接口和Mapping映射文件。这样可以省去很多的功夫，将生成的代码copy到项目工程中即可。

   使用自动生成有很多方式，可以在eclipse中安装插件，但是以下将要介绍的这种方式我认为很轻松，最简单，不需要装插件，只需要下几个jar包即可，把它们放在一个目录下面。
   其中的generatorConfig.xml是需要我们来配置的文件，配置如下：
<code>
01
<?xml version="1.0" encoding="UTF-8"?>  
02
<!DOCTYPE generatorConfiguration  
03
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"  
04
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">  
05
<generatorConfiguration>  
06
<!-- 数据库驱动-->  
07
    <classPathEntry  location="mysql-connector-java-5.1.25-bin.jar"/>  
08
    <context id="DB2Tables"  targetRuntime="MyBatis3">  
09
        <commentGenerator>  
10
            <property name="suppressDate" value="true"/>  
11
            <!-- 是否去除自动生成的注释 true：是 ： false:否 -->  
12
            <property name="suppressAllComments" value="true"/>  
13
        </commentGenerator>  
14
        <!--数据库链接URL，用户名、密码 -->  
15
        <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://192.168.1.100:3306/XMAN" userId="root" password="yunji123">  
16
        </jdbcConnection>  
17
        <javaTypeResolver>  
18
            <property name="forceBigDecimals" value="false"/>  
19
        </javaTypeResolver>  
20
        <!-- 生成模型的包名和位置-->  
21
        <javaModelGenerator targetPackage="mybatis.pojo" targetProject="src">  
22
            <property name="enableSubPackages" value="true"/>  
23
            <property name="trimStrings" value="true"/>  
24
        </javaModelGenerator>  
25
        <!-- 生成映射文件的包名和位置-->  
26
        <sqlMapGenerator targetPackage="mybatis.mapping" targetProject="src">  
27
            <property name="enableSubPackages" value="true"/>  
28
        </sqlMapGenerator>  
29
        <!-- 生成DAO的包名和位置-->  
30
        <javaClientGenerator type="XMLMAPPER" targetPackage="mybatis.dao" targetProject="src">  
31
            <property name="enableSubPackages" value="true"/>  
32
        </javaClientGenerator>  
33
        <!-- 要生成的表 tableName是数据库中的表名或视图名 domainObjectName是实体类名-->  
34
        <table tableName="tb_config" domainObjectName="Config" enableCountByExample="false"enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false"></table>
35
    </context>  
36
</generatorConfiguration>
</code>
当以上这些完成之后，只需要打开控制台，进入lib目录下，执行脚本：

[shengke@localhost lib]$ Java -jar mybatis-generator-core-1.3.2.jar -configfile generatorConfig.xml -overwrite

运行截图如下：
##注意
  本工程项目生成结构依赖于domaindemo项目结构
