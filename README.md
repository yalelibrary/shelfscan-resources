Shelfscan
=========

# Installation Steps

First, clone the three repos (shelfscan, accservices, accservices-web)

1. Clone yalelibrary/accservices
2. Clone yalelibrary/accservices-web

Import all projects into IntelliJ IDEA (or your favorite IDE). 

Make sure that all the standard Java dependecies are installed (JDK, Maven, Microsoft JDBC driver, Oracle JDBC Driver and the Primefaces JAR file). Install the JDBC driver through Maven using mvn install:install-file as documented below. 

Note: change the Oracle JDBC driver version in accservices/pom.xml if you'd like to use a different Oracle version

After installing the Java stack, build the Maven project. You'd also need to manually install these SqlServer, Oracle JDBC drivers and the custom theme for PrimeFaces:

```
cd
mvn install:install-file -Dfile=sqljdbc4.jar -DgroupId=com.microsoft.sqlserver -DartifactId=sqljdbc4 -Dversion=4.0 -Dpackaging=jar
mvn install:install-file -Dfile=bootstrap-0.0.1-SNAPSHOT.jar -DgroupId=org.primefaces.theme -DartifactId=bootstrap -Dversion=0.0.1-SNAPSHOT -Dpackaging=jar
mvn install:install-file -Dfile=/Users/odin/Downloads/ojdbc6-11.2.0.jar  -DgroupId=com.oracle -DartifactId=ojdbc6 -Dversion=11.2.0 -Dpackaging=jar

cd accservices
mvn clean install
cd ..
cd accservices-web
mvn clean install -P prod
```

Copy the resulting war file (in accservices-web/target/) to your Tomcat directory (assuming you are installing it to Tomcat). 

Browse to localhost:8080/shelfscan

# Configuration

You may need to change the path to the log file directory as well. 

Set the datasource in context.xml for blues (SqlServer) and Oracle Voyager.

Note that the current application (running on deleon) is IP restricted. 

Adjust the IP in web.xml as necessary. Make sure that you grep for IPs in the directory and change all the IPs to the server where you are running the application, otherwise the application will overwrite the data in the production database.

# Authentication

Most pages in the app are CAS restricted (in addition to IP restricted). There is no particular reason for that, but it can help enforce authorization for future purposes. Currently, the application only supports CAS authentication (there is no built in login mechanism). 
The application data comprises of just book scanning (inventory) reports, so it is not sensitive.
