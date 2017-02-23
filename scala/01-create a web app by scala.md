����һЩscala���﷨��д�˵�򵥵Ľű��󣬴��㳢����scala����webӦ�á�
��ΪĿǰ��Ҫ����spring��java��web����������������еļ�����ܳɱ�̫�ߣ�
����Ŀ�����ܹ��̳�spring��scala����������֮ǰ�ļ���ջ���ֿ��Գ���scala�����ԡ�
���Կ�ʼ��

#���Ŀ���
����������һЩscala web��ص�˵��������û�з�������ģ����ᵽ��SBT����scala��һЩ��ܣ�Ҳ��˵spring-scala��spring-boot��
spring-scala�����°汾��2013�귢���ģ���֪���ǲ��ǻ��ڸ��£�SBT�����ӻ�����ֱ�Ӽ̳�Servlet��û�����õ�spring���������յ�Ŀ�����ܹ�����ʹ��Maven��Jenkins��һ�ף����Ծ������ǻع��ϱ��У��ȴ�һ���򵥵�java web��Ŀ��

##����Java Web��Ŀ
��������Java Web��Ŀ������Maven֧�֣�����Ŀ¼�ṹ��pom�ļ���˳�ֽ���src/main/scalaĿ¼���á�
![��Ŀ�ṹͼƬ](src)

����web.xml��log4j.xml��spring-web-servlet.xml���������ļ�

###pom.xml
��Ҫ����scala-maven-plugin��scala��ص�������scalatra������akka-actor������������
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.derfy</groupId>
    <artifactId>scala-web-app</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>war</packaging>

    <name>scalaWebApp</name>
    <description>learning to build a web application based on scala</description>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
        <scala.version>2.11.8</scala.version>
    </properties>

    <repositories>
        <repository>
            <id>scalaz</id>
            <name>scalaz</name>
            <url>http://dl.bintray.com/scalaz/releases</url>
        </repository>
        <repository>
            <id>central</id>
            <name>Maven Repository Switchboard</name>
            <url>http://repo1.maven.org/maven2</url>
        </repository>
        <repository>
            <id>milestone.repo.springsource.org</id>
            <name>repo.springsource.org-milestone</name>
            <url>https://repo.springsource.org/libs-milestone</url>
        </repository>
    </repositories>

    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources/</directory>
                <includes>
                    <include>*.properties</include>
                    <include>*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources/spring</directory>
                <targetPath>spring</targetPath>
                <includes>
                    <include>*.xml</include>
                </includes>
            </resource>
        </resources>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <source>1.8</source> <!-- Դ����ʹ�õĿ����汾 -->
                    <target>1.8</target> <!-- ��Ҫ���ɵ�Ŀ��class�ļ��ı���汾 -->
                </configuration>
            </plugin>
            <plugin>
                <groupId>net.alchim31.maven</groupId>
                <artifactId>scala-maven-plugin</artifactId>
                <version>3.2.1</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>compile</goal>
                            <goal>testCompile</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>build-helper-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <id>add-source</id>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>add-source</goal>
                        </goals>
                        <configuration>
                            <sources>
                                <source>src/main/scala</source>
                            </sources>
                        </configuration>
                    </execution>
                    <execution>
                        <id>add-test-source</id>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>add-test-source</goal>
                        </goals>
                        <configuration>
                            <sources>
                                <source>src/test/scala</source>
                            </sources>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>4.2.5.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-library</artifactId>
            <version>${scala.version}</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-compiler</artifactId>
            <version>${scala.version}</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-reflect</artifactId>
            <version>${scala.version}</version>
        </dependency>
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-actors</artifactId>
            <version>${scala.version}</version>
        </dependency>
        <dependency>
            <groupId>com.typesafe.akka</groupId>
            <artifactId>akka-actor_2.10</artifactId>
            <version>2.2-M3</version>
        </dependency>
        <dependency>
            <groupId>org.scalatra</groupId>
            <artifactId>scalatra</artifactId>
            <version>2.2.0</version>
            <exclusions>
                <exclusion>
                    <groupId>com.typesafe.akka</groupId>
                    <artifactId>akka-actor</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.16</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
    </dependencies>

</project>
```

###web.xml
����web��Ŀ�����ã�ָ����������log4j��ʹ��spring��DispatcherServlet
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
		  http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
         version="2.5">

    <filter>
        <filter-name>characterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>

    <filter-mapping>
        <filter-name>characterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!-- log ����-->
    <context-param>
        <param-name>log4jConfigLocation</param-name>
        <param-value>classpath:log4j.xml</param-value>
    </context-param>
    <context-param>
        <param-name>log4jRefreshInterval</param-name>
        <param-value>60000</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.util.Log4jConfigListener</listener-class>
    </listener>

    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:/spring/spring-web-servlet.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <servlet>
        <servlet-name>scala</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextAttribute</param-name>
            <param-value>org.springframework.web.context.WebApplicationContext.ROOT</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>scala</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>

    <context-param>
        <param-name>webAppRootKey</param-name>
        <param-value>scala.webapp.root</param-value>
    </context-param>

    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <display-name>scala.webapp</display-name>

</web-app>
```

###log4j.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">

    <appender name="CONSOLE" class="org.apache.log4j.ConsoleAppender">
        <param name="encoding" value="UTF-8"/>
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%d %-5p [%c{1}] %m%n" />
        </layout>
    </appender>

    <root>
        <priority value="INFO" />
        <appender-ref ref="CONSOLE" />
    </root>

</log4j:configuration>
```

###spring-web-servlet.xml
ָ��component-scan��λ�ã�������ʵ��ʱ���֣�����src/main/java��src/main/scala���涨��������ͬ���İ�������ʱ���ܹ���springɨ�赽��
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-3.0.xsd
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
        http://www.springframework.org/schema/mvc
		http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd">

    <mvc:annotation-driven/>
    <mvc:default-servlet-handler/>

    <!-- ɨ�� -->
    <context:annotation-config/>
    <context:component-scan base-package="com.derfy"/>
    
</beans>
```

##����spring���
��src/main/java���洴��com.derfy.web.controller��������HelloJavaController.java
###HelloJavaController.java
```java
package com.derfy.web.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
@RequestMapping(path = "java")
public class HelloJavaController {

    @RequestMapping(path = "/hello")
    @ResponseBody
    public String hello() {
        return "hello java";
    }
}
```
����tomcat�����������������http://localhost:8080/java/hello�����"hello java"����Ŀ�ɹ�������

##ʵ��spring��scala��֧��
��src/main/scala���洴��com.derfy.web.controller��������HelloScalaController.scala
����java��������Զ�ת��Ϊscala�����һЩ�޸ġ�
ע������ֱ�Ӱ�java�ķ�ʽ����ͷ�����ʹ����spring��ע�⣬��RequestMapping��path��Ҫʹ���ַ������顣
###HelloScalaController.scala
```scala
package com.derfy.web.controller

import org.springframework.stereotype.Controller
import org.springframework.web.bind.annotation.{RequestMapping, ResponseBody}

@Controller
@RequestMapping(path = Array("scala"))
class HelloScalaController {

  @RequestMapping(path = Array("/hello"))
  @ResponseBody
  def hello(): String = {
    "hello scala"
  }

}
```
����tomcat���ܹ��������������������־��˵������Controller�඼��springɨ�赽�����ء�
```
2017-02-23 17:28:08,474 INFO  [RequestMappingHandlerMapping] Mapped "{[/java/hello]}" onto public java.lang.String com.derfy.web.controller.HelloJavaController.hello()
2017-02-23 17:28:08,476 INFO  [RequestMappingHandlerMapping] Mapped "{[/scala/hello]}" onto public java.lang.String com.derfy.web.controller.HelloScalaController.hello()
```
���������http://localhost:8080/scala/hello�����"hello scala"��scala����ControllerҲ���Գɹ����С�

���Լ��������PathVariableע��Ҳ��������ʹ��
###HelloScalaController.scala
```scala
package com.derfy.web.controller

import org.springframework.stereotype.Controller
import org.springframework.web.bind.annotation.{PathVariable, RequestMapping, ResponseBody}

@Controller
@RequestMapping(path = Array("scala"))
class HelloScalaController {

  @RequestMapping(path = Array("/hello"))
  @ResponseBody
  def hello(@PathVariable name: String): String = {
    "hello" + name
  }

}
```