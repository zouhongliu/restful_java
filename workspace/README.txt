This is a simple example of creating RESTful API using JAVA
------------
Installation
------------
My IOS version: 10.8.5
localhost:~ zhl$ java -version
java version "1.8.0_51"

Install Tomcat
  - download from https://tomcat.apache.org/download-80.cgi
  - Extract Eclipse into your Applicationfolder and Tomcat to your prefered location
  - Change into the apache-tomcat-6.0.20/bin directory and make all .sh files executable
  	cd <pathtoyourtomcat>/apache-tomcat-6.0.20/bin
	chmod +x *.sh
  - test if it starts  	
  	localhost:bin zhl$ ./setclasspath.sh
	localhost:bin zhl$ ./startup.sh 
	Using CATALINA_BASE:   /Users/zhl/Desktop/try/java/apache-tomcat-8.0.24
	Using CATALINA_HOME:   /Users/zhl/Desktop/try/java/apache-tomcat-8.0.24
	Using CATALINA_TMPDIR: /Users/zhl/Desktop/try/java/apache-tomcat-8.0.24/temp
	Using JRE_HOME:        /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
	Using CLASSPATH:       /Users/zhl/Desktop/try/java/apache-tomcat-8.0.24/bin/bootstrap.jar:/Users/zhl/Desktop/try/java/apache-tomcat-8.0.24/bin/tomcat-juli.jar
	Tomcat started.
 -  Verify from browser
 	http://localhost:8080/ 
 -  trouble shooting (it seems need do nothing after install SDK)
   	check log in apache-tomcat-8.0.24/logs/catalina.out
   	Exception in thread "main" java.lang.UnsupportedClassVersionError: org/apache/catalina/startup/Bootstrap : Unsupported major.minor version 51.0
     
   	Solution:
   	download lastest java JRE 8 from: https://www.java.com/en/download/mac_download.jsp
    run: 
    export JRE_HOME="/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home"   
    hint: found this path from System Preference -> Java -> Java Control Panel->Java->View->Path
	   
	-In the terminal, type
	  vi ~/.profile
	-Then add this line in the file, and save
	  export JRE_HOME="/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home" 
	-Exit the editor, then type the following command make it become effective
	  source ~/.profile 


Install Eclipse
- Download Eclipse
- Download Java JDK
  http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
- Connect Eclipse with Tomcat
  http://crunchify.com/step-by-step-guide-to-setup-and-install-apache-tomcat-server-in-eclipse-development-environment-ide/
  - Go to Window, Show View, Servers. R-click on Servers tab, New server.  
  - Open the Overview screen for the server by double clicking it.
    In the Server locations tab , select "Use Tomcat location".
  - run server by clicking green start button


-----------------
Create REST API
-----------------
http://crunchify.com/how-to-build-restful-service-with-java-using-jax-rs-and-jersey/
https://docs.oracle.com/javaee/6/tutorial/doc/gilik.html

steps
- Create project: In Eclipse => File => New => Dynamic Web Project. Name it as “RESTServerJava“.
- create and update web.xml
  Dynamic Web Project –> RightClick –> Java EE Tools –> Generate Deployment Descriptor Stub.
  <servlet>
  		<servlet-name>Jersey Web Application</servlet-name>
		<servlet-class>com.sun.jersey.spi.container.servlet.ServletContainer</servlet-class>
		<load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
	    <servlet-name>Jersey Web Application</servlet-name>
		<url-pattern>/rest/*</url-pattern>
  </servlet-mapping>
- Convert to maven project: Right click on project -> Configure -> Convert to Maven Project
- Add dependencies in pom file.
  asm.jar
  jersey-bundle.jar
  json.jar
  jersey-server.jar
- Create file Food.java
- Create file index.html



URL show index.html:
http://localhost:8080/RESTServerJava/

test URL without db:
GET http://localhost:8080/RESTServerJava/rest/food/test

get food by name(with db):
GET http://localhost:8080/RESTServerJava/rest/food/Autocomplete/food11

get food by id(with db):
GET http://localhost:8080/RESTServerJava/rest/food/55bdf4ae9b5fe93c0fda33ee

Save food to db (with db)
http://localhost:8080/RESTServerJava/rest/food?name=name1&company=company1&foodNutritionTable=calories1


-----------------------
Enable Test from Mobile
-----------------------
Get Ip of mac:
localhost:~ zhl$ ipconfig getifaddr en1
192.168.1.4

Change setting in tomcat 
- Open apache-tomcat-8.0.24/conf/server.xml
- change from 
  <Connector connectionTimeout="20000" port="8080"protocol="HTTP/1.1" redirectPort="8443"/>
  to
  <Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443" address="0.0.0.0" />
- restart tomcat, now access on your mobile device using ip address http://192.168.1.X:8080/


------------------
Other staffs(TODO)
------------------
Spring:
http://www.tutorialspoint.com/spring/spring_overview.htm

Hibernate:
http://www.tutorialspoint.com/hibernate/hibernate_examples.htm
http://www.javatpoint.com/example-to-create-hibernate-application-in-eclipse-ide

Connect to mongoDB from JAVA
http://mongodb.github.io/mongo-java-driver/2.13/getting-started/quick-tour/



