# How to deploy on tomcat server using maven
Pre-requisites
	1. Maven Server  [Get help here]
	2. Tomcat Server [Get help here]

Procedure

1. download archetype maven-archetype-webapp
	```sh 
	   mvn archetype:generate -DgroupId=com.valaxy.webapp -DartifactId=helloworld-project -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false 
    ```

1. Update pom.xml code to add maven plugin to copy artifacts onto tomcat 
   this should be under <build> 
   ```sh 
     <plugins>
     <plugin>
   			<groupId>org.apache.tomcat.maven</groupId>
   			<artifactId>tomcat8-maven-plugin</artifactId>
   			<version>2.2</version>
   		<configuration>
      		<url>http://localhost:8080/manager/text</url>
      		<server>TomcatServer</server>
      		<path>/helloworld-webapp</path>
   		</configuration>
   </plugin>
   </plugins>
   ```

1. create settings.xml for credentials 
   ```sh 
   <?xml version="1.0" encoding="UTF-8"?>
	<settings ...>
		<servers>

			<server>
				<id>TomcatServer</id>
				<username>admin</username>
				<password>password</password>
			</server>

		</servers>
	</settings>
  ```


1. Build and the project on tomcat
   ```sh
      mvn tomcat7:deploy
   ```
