# Java

**Java** - ������������� ���� ���������������� �� ������� ����������� ����������. ��������� �� java ������������� �� ��������������� � ������� ����������, � � ����������� ����-���, ������� ����������� � ����������� ����� ���������� - JVM (java virtual mashine). ��� �������, ���������������� ����� ����� ���������� `.class`. ����-��� �� �������� � ���������, ������� ��������� �� java �������� �����-��������������. ����� java, JVM �������� ������ ���������� ��� ������ ������: Scala, Groovy, Clousure � �.�.

JVM ������������ � ���� �����: JRE (java runtime environment) � JDK (java development kit). JRE �������� �� ����������� ��� ���������� ��������, � JDK ������������� �������� ������������ � ������� ��� ���������� ��������. 

���������� �� java ������������ ����� ������ c ����������� `jar`, ���������� `class`-����� � ��������������� �����. ����� ���������� ���������� �����������, � ���������������� ��������� ������� ����������:
- group id - ������������� ������ ������� (��������, ��� ������ ����� �������� ����� ������������ � ����� ������);
- artifact id - ������������� ���������;
- version - ������ ���������.

## ��������

Java ���������� ��������������� � ����������� �� ������� ��������������. ������������ �������� ���������� ���-������� �� java �������� ��������.

**�������** �������� Java-�����������, ���������� �������� ��������� �������������� ����������� �������. ������� ��������������� � ��������� ����������� �������� ������-�����. ������� �� ����� ����������� ��������������, � ������� ����������� ����� - ���������� ���������.

**��������� ���������* - ���������, �������������� ����� ������, ������� ���������� ��������� ���������� ��������� � ������������ �� ��������� ���� � ������������ � ���������, ������������ � �������������. 

**Tomcat* - ��������� ��������� � �������� �������� �����, ��������������� Apache Software Foundation. ��������� ������������ ��������� � ������������ JavaServer Pages (JSP) � JavaServer Faces (JSF). ������� �� ����� Java. Tomcat ��������� ��������� ���-����������, ���������� �� java. Tomcat ������������ � �������� ���������������� ���-�������, � �������� ������� �������� � ��������� � ���-�������� Apache HTTP Server, � ����� � �������� ���������� ��������� � �������� ���������� JBoss � GlassFish.

��������� ���� ��������:
1. ������� ���������� ������������ java � ����-��� � ���� `class`-�����.
1. � ������ ���������� �������� � ����������:
	1. ����� �������� ����������� �����������.
	1. ��������� ������� ��������� ������ ��������.
	1. ��������� �������� ����� `init()`. ���� ����� �������������� ������� � ���������� � ������ �������, �� ����, ��� ������� ������ ����������� �������. �� ���� ��������� ���� ����� `init()` ���������� ������ ���� ���.
1. ������������ ����������� �������. ������ ������ �������������� � ����� ��������� ������. ��������� �������� ����� `service()` ��� ������� �������. ���� ����� ���������� ��� ���������� ������� � ������������ ��� � ��������������� ����� ���� ����� ��� ��������� �������. ����������� �������� ������ ������������ ���������� ��� ���� �������. ���� �������� ������, ����� ��� �������� �� ����������, ���������� ����� ������������� ������ � ������ ����������� ������������ ������ ���������� �������.
1. � ������ ���� ���������� ���������� ������� �������, �� �������� ����� `destroy()`, ������� ������� ������� �� ������������. ������� ������ `init()`, ���� ����� ���� ���������� �������� �� ���� ���� ��������.

**�������������** - ��� ������� ���������� � ������� web-���������� � ���� ����������� ����������� �� �������, � ������ ������ -- � �������-����������.

**���������� �������������** - ��� ���������������� ���� ���������, ������� ����� ��������� � �������-����������.

## Maven

**Apache Maven** - ��������� ��� ������������� ������ ��������, ����������������� �� XML-����� POM (Project Object Model). Maven ��������� ���������� ��������� ������������� �������, ������������� �������� ����������� ����������. 

������ ��������� ���������� � ����� ������ ������ ���������. ������� ����������� ��� ����������� ����� ���������. Maven �������������� ���� �������. ����� ����� Maven ��������� ����������������� ������� ������ � ������� ��������, � ����� ����� ��������� �������� � ��������� �����������������.

������ pom-����� ��� ������������ ������ 3:
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>mesdt</groupId>
	<artifactId>hwspring</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>Spring Home Work</name>
	<description>Spring Home Work</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.2.1.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<start-class>hwspring.SpringHomeWorkApplication</start-class>
		<java.version>1.7</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-thymeleaf</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>
```

