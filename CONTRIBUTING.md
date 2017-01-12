Contributing to riobuild-maven-plugin
=====================================

### Deployment
---
You can add to the Maven repo by adding this to your pom.xml and executing mvn clean deploy:
```xml
<build>
<plugins>
...
<plugin>
  <groupId>com.github.github</groupId>
  <artifactId>site-maven-plugin</artifactId>
  <version>0.12</version>
  <configuration>
    <message>
      Maven artifacts for ${project.version}
    </message>
    <outputDirectory>
      ${project.build.directory}/mvn-repo
    </outputDirectory>
    <merge>true</merge>                              <!-- don't delete old artifacts -->
    <repositoryName>Maven-repo</repositoryName>      <!-- github repo name -->
    <repositoryOwner>CKCyberPack</repositoryOwner>   <!-- github username  -->
  </configuration>
  <executions>
    <execution>
      <!-- run site-maven-plugin's 'site' target as part of the build's normal 'deploy' phase -->
      <goals>
        <goal>site</goal>
      </goals>
      <phase>deploy</phase>
    </execution>
  </executions>
</plugin>
...
</plugins>
</build>

<distributionManagement>
  <repository>
    <id>internal.repo</id>
    <name>Temporary Staging Repository</name>
    <url>file://${project.build.directory}/mvn-repo</url>
  </repository>
</distributionManagement>

<properties>
  <github.global.server>github</github.global.server>
</properties>
```

In your local Maven directory (defaults to %userhome%/.m2/), you will need a `settings.xml` (make one if it does not exist) which looks like this:
```xml
<settings xmlns="http://maven.apache.org/POM/4.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>github</id>
      <password>######</password>
    </server>
  </servers>
</settings>
```
You will need to generate a personal access token in github with repo,user:email permissions to use as the password.
