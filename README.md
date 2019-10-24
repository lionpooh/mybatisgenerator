# mybatisgenerator(MBG)
mybatisgenerator sample  

use with below command (`-Dmybatis.generator.overwrite=true` overwriting mybatis generated files)
> mvn -Dmybatis.generator.overwrite=true mybatis-generator:generate

### configuration
generatorConfig.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
	<classPathEntry
		location="targetprojectpath\src\main\resources\mariadb-java-client-2.4.0-sources.jar" />

	<context id="generatortables" targetRuntime="MyBatis3">
    <!-- generator plugins -->
		<plugin type="org.mybatis.generator.plugins.RowBoundsPlugin"></plugin>
		<plugin type="org.mybatis.generator.plugins.SerializablePlugin"></plugin>

    <!-- delete default comment -->
		<commentGenerator>
		  <property name="suppressAllComments" value="true" />
		</commentGenerator>

    <!-- database connection config -->
		<jdbcConnection driverClass="org.mariadb.jdbc.Driver"
			connectionURL="jdbc:mariadb://localhost:3306/dev" userId="dev" password="asdf1234">
		</jdbcConnection>

    <!-- database models -->
		<javaModelGenerator
			targetPackage="org.lionpooh.model"
			targetProject="targetprojectpath\src\main\java">
			<property name="enableSubPackages" value="true" />
			<property name="trimStrings" value="true" />
		</javaModelGenerator>

    <!-- mapper interface -->
		<sqlMapGenerator
			targetPackage="org.lionpooh.mapper"
			targetProject="targetprojectpath\src\main\resources">
			<property name="enableSubPackages" value="true" />
		</sqlMapGenerator>

    <!-- mapper xml -->
		<javaClientGenerator type="XMLMAPPER"
			targetPackage="com.skb.cloudpc.platform.mapper"
			targetProject="targetprojectpath\src\main\java">
			<property name="enableSubPackages" value="true" />
		</javaClientGenerator>

		<!-- tables -->
		<table schema="databasename" tableName="tablename"
			domainObjectName="voname">
		</table>

	</context>
</generatorConfiguration>

```
### useful plugins

- **row plugin**  
set returned list with limited in lenght, and a start porsition can be specified
```
<plugin type="org.mybatis.generator.plugins.RowBoundsPlugin"></plugin>
```
- **serializable plugin**  
add interface `java.io.Serializable` to the java model objects generated by MBG
```
<plugin type="org.mybatis.generator.plugins.SerializablePlugin"></plugin>
```
### references
- [mybatis generator document](https://mybatis.org/generator/index.html)
