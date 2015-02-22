№ Symfony 2

## Структура проекта
	Структура проекта представлена на рисунке:
	
			\begin {figure}[h] \center
					\includegraphics[width=7cm]{symfony_project.png}
				\caption{Структура проекта Symfony2.}
				\label{fig:symfony_project}
			\end{figure}
			Проект состоит из нескольких каталогов.
			
			Каталог `app} содержит настройки вашего приложения. Файл `AppKernel.php} -- это файл, ответственный за подключение сторонних модулей. Подкаталог `Resouces} содержит кастомизацию для представлений и других настроек для данного приложения. В частности, в этом каталоге вы найдете файл для создания базового шаблона представлений. Подкаталог `config} содержит конфигурации различных подключаемых модулей. Файл `routing.yml} в нем содержит описание маршрутов.  
			
			Каталог `web} содержит точку входа в приложение. Это файл `app.php}. Вы можете создать в этой папке подкаталоги для javascript, ccs и других статических ресурсов. Файлы, расположенные в этом каталоге, напрямую доступны для пользователя сайта. В Symfony2 по умолчанию есть два окружения: `dev} (для разработки) и `prod} (готовое приложение). Окружение для разработки предоставляет панель для отслеживания количества запросов к базе, параметров http и времени работы скрипта непосредственно из браузера. Мы будем использовать окружение для разработки, точка входа для него `app\_dev.php}.
			
			Каталог `vendor} содержит модули и плагины Symfony.
	
			Каталог `src} предназначен для разработанных вами модулей. Там лежит демонстрационное приложение Acme.
		
		Конфигурационные файлы в Symfony могут храниться в разных форматах. Наиболее распространенные и удобные - в формате YAML и аннотации в php.
		
	Приложение на Symfony2 состоит из модулей, которые называются бандлы (bundles). Структура бандла устроена по принципам PSR-0 bи представлена на рисунке \ref{fig:symfony_bundle}.
	
	Для работы с базой данных в Symfony обычно используется ORM Doctrine. 
	
## Порядок установки

1. Многие действия (генерация модулей и др.) выполняются с использованием консольных команд php. Чтобы они заработали, необходимо, прописать в системную переменную `PATH} путь до php-интерпретатора. 	
					\begin {figure}[h] \center
					\includegraphics[width=12cm]{php_console.png}
				\caption{Установка переменной PATH.}
				\label{fig:php_console}
			\end{figure}	
1. Скачайте и установите Composer. 			
1. Установите модуль для работы с PHP в IDE NetBeans. Для этого пройдите в меню `<<Tools>>, <<Plugins>>} (<<Сервис>>, <<Подключаемые модули>>). Выберите плагин PHP и установите его.
				\begin {figure}[h] \center
					\includegraphics[width=12cm]{php_settings.png}
				\caption{Установка плагинов NetBeans.}
				\label{fig:php_settings}
			\end{figure}
1. Настройте модуль для работы с PHP в IDE NetBeans. Для этого пройдите в меню `<<Tools>>, <<Options>>} (<<Сервис>>, <<Параметры>>). Укажите путь до интерпретатора PHP, скачайте архивы с заготовками приложений для Zend2 и Symfony2 и укажите их в соответствующих вкладках. Укажите путь до composer.			
		  \begin {figure}[h] \center
					\includegraphics[width=7cm]{php_sett1.png}
					\includegraphics[width=7cm]{php_sett_comp.png}
					\includegraphics[width=7cm]{php_sett_symf.png}
					\includegraphics[width=7cm]{php_sett_zend.png}
				\caption{Настройка PHP.}
				\label{fig:php_sett}
			\end{figure}	
1. Создайте проект в NetBeans. Выберите `<<Приложение PHP>>}. 
				\begin {figure}[h] \center
					\includegraphics[width=12cm]{php_new.png}
				\caption{Создание проекта PHP.}
				\label{fig:php_new}
			\end{figure}	
			Выберите папку, в которой хотите создать проект. На рисунке пример для Symfony2. Укажите версию php 5.4. 
				\begin {figure}[h] \center
					\includegraphics[width=10cm]{symfony_new1.png}
				\caption{Создание проекта Symfony2.}
				\label{fig:symfony_new1}
			\end{figure}	
			На следующем шаге укажите URL, например, `http://SynfonyExample.local/}. На последнем шаге мастера выберите платформу: Symfony2 или Zend2.		
1. Настройте виртуальный хост сервера Apache на папку web. В папке проекта создайте папку папку `logs}. Пропишите хосты в файле `hosts}, как в лабораторной работе 0. Перед перезапуском сервера закройте NetBeans, потому что среда может помешать Apache писать в папку log. Перезапустите сервер.
	
	Для Symfony2 виртуальный хост выглядит так:

		```
	<VirtualHost *:80>
	 ServerAdmin webmaster@SymfonyExample.local
	 DocumentRoot "C:/WORK/projects/SymfonyExample/web
	 ServerName SymfonyExample.local
	 ServerAlias www.SymfonyExample.local
	 ErrorLog "C:/WORK/projects/SymfonyExample/log/error.log"
	 CustomLog "C:/WORK/projects/SymfonyExample/log/access.log" combined
	 <Directory "C:/WORK/projects/SymfonyExample/web">
	 AllowOverride All
	 Require all granted 
	 </Directory>
	</VirtualHost>
		```
		
1. Нажмите правой кнопкой на названии проекта в NetBeans, вызвав контекстное меню. Выберите пункт `<<Компоновщик>>}, `<<Установка (dev)>>}. Composer закачает необходимые библиотеки, если их не оказалось в каркасе приложения (скорее всего, для Zend будут скачаны библиотеки, а для Symfony ничего пока не нужно).
1. Зайдите по настроенному доменному имени (Для Symfony добавьте `<<app\_dev.php>>} в конец: `http://www.symfonyexample.local/app\_dev.php}). Вы должны увидеть, что все получилось, и порадоваться.  
			\begin {figure}[h] \center
					\includegraphics[width=10cm]{symfony_hello.png}
				\caption{Интерфейс разработчика Symfony2.}
				\label{fig:symfony_hello}
			\end{figure}
			\begin {figure}[h] \center
					\includegraphics[width=10cm]{zend_hello.png}
				\caption{Заготовка приложения на Zend2.}
				\label{fig:zend_hello}
			\end{figure}


		
### Генерация CRUD}

1.  Откройте файл `app/config/parameters.yml} и настройте базу данных.
1.  Создайте в папке `src} рядом с папкой-примером `Acme} свою папку. В примере это будет чайный магазинчик `TeaStore}.
1.  Вызовите контекстное меню на названии проекта и выберите `Symfony2}. В этом подменю три пункта: очистка кэша, прогрев кэша (заполнение кэша) и <<Выполнить команду>> (графический интерфейс для доступа к консоли Symfony2). Выберите этот пункт меню.
1. Мы видим список всех доступных команд Symfony2. Кроме того, для каждой из них есть подстказки с примерами. Нам необходимо вызвать команду `<<generate:bundle>>} для создания нового модуля. Начните писать название команды в поле <<Фильтр>>. Выберите команду из списка. В Поле <<Параметры>> укажите `<<--namespace=TeaStore/CupsBundle --format=annotation>>}. Это означает, что наш бандл будет находиться в нашем пространстве имен `TeaStore} и называться `CupsBundle}. Запускаем команду.
			\begin {figure}[h] \center
					\includegraphics[width=7cm]{symfony_command1.png}
				\caption{Создания бандла.}
				\label{fig:symfony_command1}
			\end{figure}
		У нас спрашивают название бандла (оно автоматически генерируется из пространства имен) и папку, куда мы хотим генерировать. Просто нажимаем <<Enter>> для продолжения. Symfony спрашивает, сгенерировать ли всю структуру каталогов. Соглашаемся.
			
			```
			Do you want to generate the whole directory structure [no]? y
			```
			Еще одно подтверждение - и запустилась генерация бандла. Далее необходимо подтвердить добавление нового бандла в `appKernel.php} и в `routing.yml}. Соглашаемся. Зайдите в эти файлы, и убедитесь, что новый бандл добавлен.
			\begin {figure}[h] \center
					\includegraphics[width=7cm]{symfony_bundle.png}
				\caption{Структура бандла.}
				\label{fig:symfony_bundle}
			\end{figure}			
			Команда создала всю структуру каталогов, которая может нам понадобиться, а также контроллер и представление (в формате twig). Посмотрите, как устроены эти файлы. Их работу можно посмотреть, зайдя по адресу:
			
			`http://www.symfonyexample.local/app\_dev.php/hello/Vasia}
			
1. Создайте класс модели. Для этого создайте внутри бандла папку `Entity}. В этой папке создайте класс вашей модели. В нашем примере это `Cup}. Обратите внимание, что класс и файл должны называться одинаково. Создадим простейший класс и опишем необходимые нам поля. Doctrine умеет генерировать базу по объектному описанию. Поскольку вы работаете с уже существующей базой, название полей класса должны совпадать с полями базы. Кроме того, по умолчанию каждая таблица, с которой вы работаете, должна иметь уникальный идентификатор с названием `\$id}. 
	
	Возможные типы Doctrine для полей в аннотациях
	
	\begin{table}[h]
		\centering
			\begin{tabular}{l|l|l}
				\textbf{Тип Doctrine} & \textbf{Тип SQL} & \textbf{Тип php} \\ \hline
				string & VARCHAR & string\\
    integer& INT & integer\\
    smallint& SMALLINT & integer\\
    bigint& BIGINT & string\\
    boolean& boolean & boolean\\
    decimal& DECIMAL & double\\
    date& DATETIME & DateTime object\\
    time& TIME & DateTime object\\
    datetime& DATETIME/TIMESTAMP & DateTime object\\
    text& CLOB & string\\
    object& CLOB & object \\
    array& CLOB & object \\
    float& Float (Double Precision) & double\\ 
			\end{tabular}
		\caption{Название типов Doctrine}
		\label{tab:DoctrineTypes}
	\end{table}


	```
	<?php
	namespace TeaStore\CupsBundle\Entity;
	use Doctrine\ORM\Mapping as ORM;

	/**
	 * @ORM\Entity
	 * @ORM\Table(name="cup")
	 */
	class Cup
	{
		/**
		 * @ORM\Column(type="integer")
		 * @ORM\Id
		 * @ORM\GeneratedValue(strategy="AUTO")
		 */
		protected $id;

		/**
		 * @ORM\Column(type="string", length=100)
		 */
		protected $name;

		/**
		 * @ORM\Column(type="integer")
		 */
		protected $d;

		/**
		 * @ORM\Column(type="integer")
		 */
		protected $height;
		
		/**
		 * @ORM\Column(type="boolean")
		 */
		protected $has_plate;
	}
	```

		Запустим генерацию сущностей. Это делается командой  `doctrine:generate:entities TeaStore/CupsBundle/Entity/Cup}.
		
		Посмотрите, как изменился класс сущности. Команду можно запускать несколько раз, после каждого изменения.
		
	1. Запустите генерацию CRUD командой  `doctrine:generate:crud --entity=TeaStoreCupsBundle:Cup}.
		
			Дальше идет вопрос о том, надо ли нам генерировать операции добавления-изменения, или только простмотра. Мы делаем полноценный GRUD, так что нажимаем \textbf{<<y>>}. Далее идет вопрос о том, какой вид конфигурационных файлов будет использоваться. Выбираем значение оп умолчанию - аннотации. Следующим шагом можно задать префикс маршрута. Оставляем по умолчанию. Подтверждаем генерацию и подключение модуля.
			
			На защите лабораторной работы необходимо разбираться в содержимом сгенерированных файлов. При генерации создаются следующие файлы:
		
		\begin{itemize}
		- Контроллер  `src/TeaStore/CupsBundle/Controller/CupController.php}.  В контроллере кроме собственно действий прописаны маршруты.
		- Класс формы для удаления/изменения записей  `src/TeaStore/CupsBundle/Form/CupType.php}
		- Каталог для представлений  `src/TeaStore/CupsBundle/Resources/views/Cup}  и четыре представления в нем для отображения списка, отображения одной записи, добавления и редактирования.
		\end{itemize}
			
		Вносится изменение в конфигурационный файл маршрутов приложения `app/config/routing.yml}
					
		Все это происходит автоматически. Зайдите по новому url   `symfonyexample.local/app\_dev.php/cup}. Убедитесь, что функциональность работает. 			
	1. Настройте представления twig. Сначала зайдите в файл   `app/Resources/views/base.html.twig}. Это файл layout, в котором необходимо прописать шапку, футер и другие элементы, которые присутствуют на всех страницах, а также сформировать блоки, которые будут заменены в других шаблонах. Простейший пример приведен ниже.

	```
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="UTF-8" />
			<title>{% block title %}Welcome!{% endblock %}</title>
			{% block stylesheets %}{% endblock %}
			<link rel="icon" type="image/x-icon" 
							href="{{ asset('favicon.ico') }}" />
		</head>
		<body>
			{% block body %}{% endblock %}
			{% block javascripts %}{% endblock %}
		</body>
	</html>
	```

Теперь пройдите в файлы представлений для модуля CRUD, установите наследование от главного шаблона и внесите необходимые изменения. Далее приведен простейший пример наследования twig для просмотра записи.

	```
	{% extends '::base.html.twig' %}
	{% block body -%}
	<h1>Cup</h1>
	<table class="record_properties">
			<tbody>
					<tr> <th>Id</th> <td>{{ entity.id }}</td> </tr>
					<tr> <th>Name</th> <td>{{ entity.name }}</td> </tr>
					<tr> <th>D</th> <td>{{ entity.d }}</td> </tr>
					<tr> <th>Height</th> <td>{{ entity.height }}</td> </tr>
					<tr> <th>Has_plate</th> <td>{{ entity.hasplate }}</td> </tr>
			</tbody>
	</table>

	<a href="{{ path('cup') }}"> К списку </a>
	<a href="{{ path('cup_edit', { 'id': entity.id }) }}">
				Редактировать запись</a>
	 {{ form(delete_form) }}
	{% endblock %}
	```

Необходимо настроить верстку из самой первой лабораторной работы.