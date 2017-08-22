# Google Cloud Endpoint
Generate Android Client libraries with Maven  
Generate Swagger file for Endpoints section on Google Cloud Console. This section is usefull to see all the calls to your API and manage the externals authorizations given to your clients   
Deploy the code on your Google Cloud Server

## Requierments
  * [gcloud](https://cloud.google.com/sdk/gcloud/) command-line tool. Follow the guide to init the tool.
  * [mvn](https://maven.apache.org/)
  * [Endpoints framework tools](http://search.maven.org/remotecontent?filepath=com/google/endpoints/endpoints-framework-tools/2.0.0-beta.11/endpoints-framework-tools-2.0.0-beta.11.zip)
  * Java 7
  
## Project structure
Project Name  
|-- src  
|&nbsp;&nbsp;&nbsp;&nbsp;|-- main  
|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|-- java  
|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|-- com.example.endpoints  
|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|-- myEndpoint.java  
|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|-- webapp  
|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|-- WEB-INF  
|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|-- appengine.xml  
|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|-- web.xml  
|-- pom.xml  

## Gcloud
Execute this command to download the package  
>gcloud components install app-engine-java

## In pom.xml
You need a tool to execute a script and build your endpoints.  

 ```
 <plugin>  
   <groupId>com.google.cloud.tools</groupId>  
   <artifactId>appengine-maven-plugin</artifactId>  
   <version>1.3.1</version>  
 </plugin>
 ```  
 
 ```
 <plugin>
    <groupId>com.google.cloud.tools</groupId>
    <artifactId>endpoints-framework-maven-plugin</artifactId>
    <version>1.0.0</version>
    <configuration>
        <!-- plugin configuration -->
        <hostname>YOUR-PROJECT-ID.appspot.com</hostname>
    </configuration>
</plugin>
```

```
<dependency>
    <groupId>com.google.endpoints</groupId>
    <artifactId>endpoints-framework</artifactId>
    <version>2.0.7</version>
</dependency>
```

```
<plugin>
    <groupId>com.google.appengine</groupId>
    <artifactId>appengine-maven-plugin</artifactId>
    <version>1.9.54</version>
</plugin>
```

## In web.xml

```
<servlet>
    <servlet-name>EndpointsServlet</servlet-name>
    <servlet-class>com.google.api.server.spi.EndpointsServlet</servlet-class>
    <init-param>
        <param-name>services</param-name>
        <param-value>com.example.helloendpoints.Greetings</param-value>
    </init-param>
    <init-param>
        <param-name>restricted</param-name>
        <param-value>false</param-value>
    </init-param>
</servlet>
<servlet-mapping>
    <servlet-name>EndpointsServlet</servlet-name>
    <url-pattern>/_ah/api/*</url-pattern>
</servlet-mapping>
```

## How to
  1. Change var corresponding to your package (in tree it's com.example.endoints)
  2. Change var corresponding to your project's name
  3. Change var corresponding to your project's version
  4. Execute the script with this command 
>./script  

## Results
All endpoints are generated in folder generatedEndpoints in the root of your project. There are .zip and unzip file. Script execute `>mvn install` for each endpoint and generate a `jar`. Use this `jar` in your android project.  
You can see Endpoints section in https://console.cloud.google.com/endpoints?project=[YOUR-PROJECT-ID]
The project is also deployed on your server.
You can deploy cron tasks and queue (you have to uncomment line)

## Documentation
https://cloud.google.com/appengine/docs/standard/java/tools/using-maven
https://cloud.google.com/appengine/docs/standard/java/tools/maven
https://cloud.google.com/endpoints/docs/frameworks/java/about-cloud-endpoints-frameworks
https://cloud.google.com/endpoints/docs/frameworks/java/generate-client-libraries-android
https://cloud.google.com/endpoints/docs/frameworks/java/adding-api-management
