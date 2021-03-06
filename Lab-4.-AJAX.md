# Лабораторная работа 4. AJAX

## Цели работы

- Познакомиться с технологией AJAX.
- Изучить библиотеку JQuery.

## Задание

1. Реализовать AJAX-загрузку различных фрагментов страницы.
2. Реализовать AJAX-отправку формы.

Работа выполняется на базе лабораторной 2 или лабораторной 3 (по выбору студента). Конкретное задание, соответствующее вашему варианту, согласуйте с преподавателем.

## Краткие теоретические сведения

**JavaScript** - скриптовый язык для реализации интерактивности в браузерах. 

**AJAX (асинхронный JavaScript и XML)** - технология для генерации содержимого страницы без полной перезагрузки. Это не самостоятельная технология, а концепция использования нескольких смежных технологий. AJAX базируется на двух основных принципах:
- использование технологии динамического обращения к серверу "на лету", без перезагрузки всей страницы полностью, например:
	- с использованием XMLHttpRequest (основной объект);
	- через динамическое создание дочерних фреймов или окон (например, так реализуется авторизация через социальные сети на различных сайтах);
	- через динамическое создание тега `<script>`;
	- через динамическое создание тега `<img>`, как это реализовано в google analytics.
- использование DHTML для динамического изменения содержания страницы.

Работа технологии AJAX в классическом случае состоит из двух стадий. Первая стадия - это формирование запроса и отправка запроса на сервер. Вторая стадия - это	обработка события на получение ответа от сервера. Данные операции выполняются асинхронно, то есть между стадиями браузер не зависает в ожидании ответа.

**XML** - довольно объемный формат, данные в нем занимают много места, поэтому для передачи данных по сети в современном AJAX используется JSON.

**JSON** - это язык описания данных, основанный на Java Script. Состоит из следующих типов элементов.
- Объект - неупорядоченный набор пар ключ/значение. Объект начинается с `{` (открывающей фигурной скобки) и заканчивается `}` (закрывающей фигурной скобкой). Каждое имя сопровождается `:` (двоеточием), пары ключ/значение разделяются `,` (запятой).
- Массив - упорядоченная коллекция значений. Массив начинается с `[` (открывающей квадратной скобки) и заканчивается `]` (закрывающей квадратной скобкой). Значения разделены `,` (запятой). 
- Значение может быть строкой в двойных кавычках, числом, `true`, `false`, `null`, объектом или массивом. Эти структуры могут быть вложенными. 

**jQuery** - ключевая библиотека JavaScript. Фактически, это библиотека "стандартных" функций языка. Библиотека кросс-браузерная. Библиотека jQuery предназначена прежде всего для удобного поиска и манипулирования элементами на веб-странице. После загрузки страницы библиотека позволяет подключить к элементам дополнительную функциональность. Функция `jQuery` (или `$`) принимает строку, содержащую CSS селектор, которая затем используется для поиска соответствующих элементов.

 [Cheat list jQuery](/mesdt/course/wiki/Cheat-list-jQuery)

Достоинства:
- значительное облегчение манипулирования объектами;
- кросс-браузерная совместимость;
- возможность эффективного разделения разметки и кода на JavaScript;
- огромное сообщество, большое количество плагинов (некоторые некачественные);
- повсеместное использование.

Недостатки:
- дополнительный объем (незначительно для минимизированной версии);
- скорость работы (незначительно для современных браузеров);
- часто - обратная несовместимость на уровне плагинов (плагины оказываются привязаны к узкому диапазону версий, и могут не работать не только на старых версиях библиотеки, но и на новых; часто приходится отказываться от использования плагинов, несовместимых между собой).

## Порядок выполнения

Работа выполняется на базе лабораторной 2 или лабораторной 3 (по выбору студента). В качестве примера рассматривается поиск студента по части фамилии.

Рассмотрим на примере получения списка оценок по id студента.

1. Разработать маршрут и реализовать действие, которое возвращает результат работы в формате json.
	
	- На PHP Silex сформировать ответ на языке json можно с помощью соответствующего метода:

		```php
		public JsonResponse json(mixed $data = array(), int $status = 200, array $headers = array())
		```

		Пример:

		```php
		$sapp->get('/students/{id}/grades', function ($id) use ($sapp) {
			/**@var $conn Connection */
			$conn = $sapp['db'];
			$subjects = $conn->fetchAll('select * from subjects');
			$scores = $conn->fetchAll('select * from scores where student_id = ?', [$id]);
			$scorez = [];
			foreach ($scores as $score) {
				$scorez[$score['subject_id']] = $score['score'];
			}
			return $sapp->json(array('subjects'=>$subjects,'scorez'=>$scorez));
		});
		```
		Подробный пример смотрите в [hw4_php](https://github.com/mesdt/hw4_php). 
			
	- На Java Spring Boot не требуется специально преобразовывать объекты в json, достаточно просто вернуть их из метода-действия:
	
		```java
			@ResponseBody
			@RequestMapping(method = RequestMethod.GET, value = "/students/{id}/scores")
			public Object gradesStudent(@PathVariable Long id) {
				Student student = hw2.student(id);
				return hw2.scoresAsStr(student);
			}
		```
		Подробный пример смотрите в [hw4_java](https://github.com/mesdt/hw4_java). 
			- Добавлено два маршрута и два соответствующих действия в контроллер. 
			- Добавлено два метода в сервис (редактирование имени студентов и получение списка оценок в формате, где ключом является название предмета, а не объект предмета).
			- Добавлен js-файл для ajax-запросов
			- Изменен шаблон `students`.
	
2. Внести изменения в представления, добавив форму, которая будет отправлять данные с помощью AJAX и получать результат.
	
3. Подключить jQuery.

	```javascript
	 <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>	
	```
4. Создать свой файл скриптов. С использованием JQuery написать AJAX-запрос.

**Замечание:** для отладки скриптов используйте вкладки "Сеть" (для просмотра результатов запросов) и "Консоль" (для просмотра ошибок JavaScript) в инструментах вашего браузера.

### Пример из проекта [hw4_java](https://github.com/mesdt/hw4_java), получение списка оценок. 
Создаем кнопку в шаблоне:

```html
	<button class="btn btn-default btn-grades" th:attr="data-id=${student.id}">Показать оценки</button>
```

Где-то в шаблоне создаем место, куда будем выводить информацию. Как правило, такие места имеют уникальный `id`. Вы можете выводить одну и ту же информацию сразу в несколько мест, используя атрибут `class` вместо `id`.

```html
	<div class="col-md-4" id="grades">		
	</div>
```

Создаем событие, обрабатывающее клик на кнопку:

```javascript
	$(document).ready(function(){    
	...
	$(".btn-grades").click(function(){
			id = $(this).data("id"); // Получаем значение id студента из поля data кнопки
			$.ajax({ // Отправляем запрос
							type: "GET",
							url: "/students/"+id+"/scores"
					})
					.done(function( data ) { // Разбираем полученные данные и пишем в блок grades
							$("#grades").html( "<h3>Оценки</h3>" );
							for (var subject in data) {
									$("#grades").append( subject+": "+ (data[subject] ? data[subject] : "-")+"<br>" );
							}

					});		
	});
	}) ;
```

## Дополнительное задание на повышение рейтинга

Вы можете реализовать дополнительные действия через AJAX (поиск, сортировка, другое, зависит от предметной области), сделать красивое оформление и уместные сообщения при обработке запросов.

## Порядок защиты работы

При защите лабораторной необходимо продемонстрировать работу двух функций, которые используют AJAX. Необходимо уметь доказать, что это AJAX. В отчете необходимо привести код контроллера, модели и представления (можно не полностью, только добавленные методы), а также текст javascript.

## Ссылки на документацию
- [Официальная документация JSON на русском!](http://www.json.org/json-ru.html)
- [jQuery API](http://api.jquery.com/)
- [jQuery AJAX](http://api.jquery.com/jquery.ajax/)
- [Документация по работе с json в PHP Silex](http://silex.sensiolabs.org/doc/cookbook/json_request_body.html)