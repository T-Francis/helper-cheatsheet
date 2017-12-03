**Maven**

| [Official Site ](https://example.com/) | [config example source](https://source.html) |
| :---: | :---: |

![](../logos/logos-v1-128x128.png)

### Installation

+ Example
```bash

```


### Config Example

+ Example
```bash

```

```plain text

```

```xml

```

### Deploy Plugin Example

+ Tomcat Manager Script Deployement

Will deploy the app under tomcat server /webapps and a distribution repository

Maven User Settings
```xml
	<servers>

	   <server>
	       <id>hostName</id>
	       <username>tomcatUserManager</username>
	       <password>password</password>
	   </server>
	   
	</servers>
```

Pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<!-- Group Id (ex : com.yourname) -->
	<groupId>fr.aliart</groupId>
	<!-- Main package name (ex : appname ) -->
	<artifactId>demo</artifactId>
	<!-- App Name & Description -->
	<name>Demo</name>
	<description>Demo</description>
	<!-- App Version -->
	<version>0.1</version>
	<!-- App packaging -->
	<packaging>war</packaging>

	<!-- PROPERTIES -->	
	<properties>
		<!-- ... /your config ... -->
	</properties>

	<!-- DEPENDENCIES -->
	<dependencies>
		<!-- ... /your config ... -->
	</dependencies>

	<!-- BUILD -->
	<build>	

		<!-- ... /your config ... -->

		<!-- PLUGIN -->
		<plugins>

			<!-- ... /your config ... -->

			<!-- tomcat plugin -->
			<plugin>
				<groupId>org.codehaus.mojo</groupId>
				<artifactId>tomcat-maven-plugin</artifactId>
				<configuration>
					<url>http://192.168.0.1:8080/manager/text</url>
					<server>tomcatManagerCredentials</server>
					<path>/bibliospring</path>
					<!-- update settings on true to allow "re-deployment" without undeploying the application -->
					<update>true</update>
				</configuration>
			</plugin>

		</plugins>

	</build>

</project>
```

+ SSH Wagon Deployement

Will deploy the app under tomcat server /webapps and a distribution repository
Remember that you may have to set different credentials where you wanna upload the distribution repository and tomcat/manager regarding your configuration

Maven User Settings
```xml
	<servers>

	   <server>
	       <id>hostName</id>
	       <username>userName</username>
	       <password>password</password>
	   </server>
	   
	</servers>
```

Pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<!-- Group Id (ex : com.yourname) -->
	<groupId>fr.aliart</groupId>
	<!-- Main package name (ex : appname ) -->
	<artifactId>demo</artifactId>
	<!-- App Name & Description -->
	<name>Demo</name>
	<description>Demo</description>
	<!-- App Version -->
	<version>0.1</version>
	<!-- App packaging -->
	<packaging>war</packaging>

	<!-- PROPERTIES -->	
	<properties>
		<!-- ... /your config ... -->
	</properties>

	<!-- DISTRIBUTION MANAGEMENT -->	
	<distributionManagement>

		<!-- wagon ssh user repository settings -->
		<repository>
			<id>UserRepositoryCredentials</id>
			<uniqueVersion>true</uniqueVersion>
			<name>Demo Repository</name>
				<!-- On original configutation, the SCP protocol is used and result sith some dowloading issue on deploy, change it on sftp fix it
				<url>scp://192.168.0.1/home/user/repository/path</url> -->
	 			<url>sftp://192.168.0.1/home/user/repository/path</url>
			<layout>default</layout>
		</repository>

	</distributionManagement>

	<!-- DEPENDENCIES -->
	<dependencies>

		<!-- ... /your config ... -->

		<!-- wagon ssh dependancies https://mvnrepository.com/artifact/org.apache.maven.wagon/wagon-ssh -->
 		<dependency>
			<groupId>org.apache.maven.wagon</groupId>
			<artifactId>wagon-ssh</artifactId>
			<version>3.0.0</version>
		</dependency> -->

	</dependencies>

	<!-- BUILD -->
	<build>	

	<finalName>${project.artifactId}</finalName>

		<!-- EXTENSIONS -->
		<extensions>

			<!-- ... /your config ... -->

		    <!-- wagon ssh extension -->
		    <extension>
		    	<groupId>org.apache.maven.wagon</groupId>
		        <artifactId>wagon-ssh</artifactId>
		        <version>2.8</version>
		    </extension>

	    </extensions>

		<!-- PLUGIN -->
		<plugins>

			<!-- ... /your config ... -->

			<!-- wagon ssh plugin -->
 			<plugin>
				<groupId>org.codehaus.mojo</groupId>
				<artifactId>wagon-maven-plugin</artifactId>
				<version>1.0</version>
				<executions>
					<execution>
						<phase>deploy</phase>
						<goals>
							<goal>upload-single</goal>
						</goals>
 						<configuration>
					    	<serverId>UserRepositoryCredentials</serverId>
					     	<fromFile>${project.build.directory}/${project.artifactId}.${project.packaging}</fromFile>
					     	<!-- On original configutation, the SCP protocol is used and result sith some dowloading issue on deploy, change it on sftp fix it
					     	<url>scp://192.168.0.1/opt/tomcat/webapps</url> -->
					     	<url>sftp://192.168.0.1/opt/tomcat/webapps</url>
					    </configuration>
					</execution>
				</executions>
			</plugin>

		</plugins>

	</build>

</project>
```