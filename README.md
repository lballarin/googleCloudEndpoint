# Google Cloud Endpoint Android Client
Generate Android Client libraries with Maven 

## Requierments
  * [gcloud](https://cloud.google.com/sdk/gcloud/) command-line tool. Follow the guide to init the tool.
  * [mvn](https://maven.apache.org/)
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
All endpoints are generated in fodler generatedEndpoints in a root of your project. There are .zip and unzip file. Script execute `>mvn install` for each endpoint and generate a `jar`. Use this `jar`in your android project.

## Documentation
https://cloud.google.com/appengine/docs/standard/java/tools/using-maven
https://cloud.google.com/endpoints/docs/frameworks/java/about-cloud-endpoints-frameworks
https://cloud.google.com/endpoints/docs/frameworks/java/generate-client-libraries-android