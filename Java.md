# Java

**Java** - универсальный язык программирования со строгой статической типизацией. Программы на java компилируются не непосредственно в команды процессора, а в специальный байт-код, который выполняется в специальной среде выполнения - JVM (java virtual mashine). Как правило, скомпилированные файлы имеют расширение `.class`. Байт-код не привязан к платформе, поэтому программы на java являются кросс-платформенными. Кроме java, JVM является средой выполнения для других языков: Scala, Groovy, Clousure и т.д.

JVM поставляется в двух видах: JRE (java runtime environment) и JDK (java development kit). JRE содержит всё необходимое для выполнения программ, а JDK дополнительно содержит документацию и утилиты для разработки программ. 

Библиотеки на java представляют собой архивы c расширением `jar`, содержащие `class`-файлы и вспомогательные файлы. Такие библиотеки называются артефактами, и идентифицируются следующим набором параметров:
- group id - идентификатор группы пакетов (например, все пакеты одной компании могут принадлежать к одной группе);
- artifact id - идентификатор артефакта;
- version - версия артефакта.

## Сервлеты

Java изначально разрабатывалась с ориентацией на сетевое взаимодействие. Классическим способом реализации веб-сервера на java являются сервлеты.

**Сервлет** является Java-интерфейсом, реализация которого расширяет функциональные возможности сервера. Сервлет взаимодействует с клиентами посредством принципа запрос-ответ. Сервлет не может выполняться самостоятельно, и требует специальной среды - контейнера сервлетов.

**Контейнер сервлетов* - программа, представляющая собой сервер, который занимается системной поддержкой сервлетов и обеспечивает их жизненный цикл в соответствии с правилами, определёнными в спецификациях. 

**Tomcat* - контейнер сервлетов с открытым исходным кодом, разрабатываемый Apache Software Foundation. Реализует спецификацию сервлетов и спецификацию JavaServer Pages (JSP) и JavaServer Faces (JSF). Написан на языке Java. Tomcat позволяет запускать веб-приложения, написанные на java. Tomcat используется в качестве самостоятельного веб-сервера, в качестве сервера контента в сочетании с веб-сервером Apache HTTP Server, а также в качестве контейнера сервлетов в серверах приложений JBoss и GlassFish.

Жизненный цикл сервлета:
1. Сервлет собирается компилятором java в байт-код в виде `class`-файла.
1. В случае отсутствия сервлета в контейнере:
	1. Класс сервлета загружается контейнером.
	1. Контейнер создает экземпляр класса сервлета.
	1. Контейнер вызывает метод `init()`. Этот метод инициализирует сервлет и вызывается в первую очередь, до того, как сервлет сможет обслуживать запросы. За весь жизненный цикл метод `init()` вызывается только один раз.
1. Обслуживание клиентского запроса. Каждый запрос обрабатывается в своем отдельном потоке. Контейнер вызывает метод `service()` для каждого запроса. Этот метод определяет тип пришедшего запроса и распределяет его в соответствующий этому типу метод для обработки запроса. Разработчик сервлета должен предоставить реализацию для этих методов. Если поступил запрос, метод для которого не реализован, вызывается метод родительского класса и обычно завершается возвращением ошибки инициатору запроса.
1. В случае если контейнеру необходимо удалить сервлет, он вызывает метод `destroy()`, который снимает сервлет из эксплуатации. Подобно методу `init()`, этот метод тоже вызывается единожды за весь цикл сервлета.

**Развертывание** - это процесс размещения и запуска web-приложения и всех необходимых компонентов на сервере, в данном случае -- в сервлет-контейнере.

**Дескриптор развертывания** - это конфигурационный файл артефакта, который будет развернут в сервлет-контейнере.

## Maven

**Apache Maven** - фреймворк для автоматизации сборки проектов, специфицированных на XML-языке POM (Project Object Model). Maven позволяет эффективно управлять зависимостями проекта, автоматически скачивая необходимые библиотеки. 

Многие артефакты используют в своей работе другие артефакты. Вручную отслеживать эти зависимости очень трудоемко. Maven автоматизирует этот процесс. Кроме этого Maven позволяет стандартизировать условия сборки и запуска проектов, а также имеет множество плагинов с различной функциональностью.

Пример pom-файла для лабораторной работы 3:
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

