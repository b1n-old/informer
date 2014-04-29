Maven Plugin that sends build information to a server for analysis.

Information sent to the server:
* Host
* User
* JVM version
* Encoding
* Project/Module build time
* Is the build a deploy?
* Were tests skipped?

The project has 2 parts:
* Informer: The Maven Plugin
* Receiver: The Server

## Informer
To use the plugin you have to configure it in your pom.xml file:
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.b1n.informer</groupId>
      <artifactId>maven-informer-plugin</artifactId>
      <version>4.0.0</version>
      <executions>
        <execution>
          <id>start</id>
          <phase>validate</phase>
          <goals>
            <goal>informer</goal>
          </goals>
          <configuration>
            <action>start</action>
          </configuration>
        </execution>

        <execution>
          <id>end</id>
          <phase>install</phase>
          <goals>
            <goal>informer</goal>
          </goals>
          <configuration>
            <action>end</action>
          </configuration>
        </execution>
      </executions>

      <configuration>
        <server>${SAVE_URL}</server>
        <dataSenderClassName>org.b1n.informer.ds.PostHttpDataSender</dataSenderClassName>
        <minBuildTime>1000</minBuildTime>
        <maxAttempts>1</maxAttempts>
      </configuration>
    </plugin>
  </plugins>
</build>
```

Configuration options:
* Server: The HTTP URL the _Receiver_ is waiting to get data from the _Informer_

## Receiver
The server.

(...)

