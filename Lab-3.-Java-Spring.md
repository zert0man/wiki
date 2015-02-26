# Лабораторная работа 3. Java Spring Boot

## Цели работы
- Познакомиться с фреймворком Spring Boot и уровнем абстракции базы данных Java Persistence Api.
- Изучить паттерн ORM и Dependency Injection на примере Spring Boot.

## Краткие теоретические сведения

- [Java и сборщик проектов Maven](/mesdt/course/wiki/Java) 
- [Java Spring](/mesdt/course/wiki/Java-Spring) 
- [Java Persistence Api](/mesdt/course/wiki/JPA) 

### Java Spring Boot

**Java Spring** - огромный фреймворк для языка Java. Приложение на Java Spring представляет собой контейнер компонентов, которые называаются бинами (beans) или артефактами (artefacts). Фактически, это просто классы на языке java/


### Java Persistence Api
 

## Порядок выполнения
- [Репозиторий с примером обработки REST-запросов ](https://github.com/mesdt/calculator) (lk jpyfrjvktybz)
- [Репозиторий с примером лабораторной работы ](https://github.com/mesdt/hw2)

** Рекомендуемая версия: Java 1.8 ** Возможно использование Java 1.6 и выше, но лучше обновитесь, новая Java круче!

### Установка и настройка 
1. Установите Maven.  Для linux это можно сделать командой командой `apt-get install maven`. Для остальных операционных систем - смотрите на [официальном сайте](http://maven.apache.org/).
2. Зайдите на [cервис для создания заготовки проекта Spring Boot](http://start.spring.io/). Изучите доступные параметры. Создайте проект. Для этого задайте в форме основные параметры для конфигурационного фалйа Maven. Введите идентификатор группы (например, `mesdt`) и идентификатор артефакта (например, `hw3`). Дополнительно можете задать имя проекта, описание и другие параметры. Отметьте необходимые зависимости: web для генерации веб-приложений, шаблонизатор Thymeleaf, библиотеку для работы с данными JPA и драйвер базы данных MySQL. Нажмите кнопку генерации пакета и скачайте архив.  
3. В скачанном архиве находится заготовка проекта на Spring Boot. Распакуйте архив. Изучите структуру каталогов:
```
└── src
    └── main
    |   └── java
    |   |   └── yourProjectName
	|	|	|	└── SpringHomeWorkApplication.java
	|	└── Resources
	|		└── static
	|		└── templates
	|		└── application.properties
	└── test
        └── java
            └── yourProjectName	
				└── SpringHomeWorkApplicationTests.java
	pom.xml		
```

- `pom.xml` - файл конфигурации Maven;
- `test` - директория для тестов, в этом курсе рассматриваться не будет;
- `main` - каталог, содержащий исходные коды приложения, в подкаталоге `java/yourProjectName` будут располагарться файлы с исходным кодом.
- `static` - каталог для статических ресурсов;
- `templates` - каталог для файлов представлений;
- `application.properties` - конфигурационный файл Spring Boot;
- `SpringHomeWorkApplication.java` - главный файл проекта.

### Подключение к базе данных

### Подключение шаблонов

## Порядок защиты работы

## Ссылки на скачивание инструментов
- Maven [http://maven.apache.org/](http://maven.apache.org/)
- Сервис для создания заготовки проекта Spring Boot [http://start.spring.io/](http://start.spring.io/)

## Ссылки на документацию
- Документация по Java 8 [http://docs.oracle.com/javase/8/](http://docs.oracle.com/javase/8/)
- Документация по шаблонизатору Thymeleaf [http://www.thymeleaf.org/](http://www.thymeleaf.org/)