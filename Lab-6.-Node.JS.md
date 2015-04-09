# Лабораторная работа 6. Node.JS

## Цели и задачи

**Цель работы:** освоить основы работы с фреймворком Node.js.

**Задача работы:** разработать приложение на Node.js, реализующее CRUD объектов из базы данных MongoDB. 

## Краткие теоретические сведения

**Node.js** - программная платформа, основанная на движке V8, превращающая JavaScript из узко специализированного языка в язык общего назначения. **V8 JavaScript Engine** - движок JavaScript, используемый в браузере Chrome. В основе Node.js лежит событийно-ориентированное и асинхронное (или реактивное) программирование с неблокирующим вводом/выводом.

За установку модулей в Node.js отвечает установщик пакетов npm (node package manager).

Для выполнения лабораторной работы потребуются следующии плагины Node.js.
- [Express](http://expressjs.com/) - web-фреймворк для работы с маршрутизацией.
- [Path](https://nodejs.org/api/path.html) - модуль для обработки путей, в частности, для подключения статических ресурсов.
- Шаблонизатор на выбор:
	- [Swig](http://paularmstrong.github.io/swig/);
	- [Jade](http://jade-lang.com/).
- [Mongoose](http://mongoosejs.com/docs/guide.html) - ODM

Подробнее про эти модули вы можете прочитать в документации.

## Порядок работы
1. Если вы не используете виртуальную машину mesdt, [скачайте](http://nodejs.org/download) и установите Node.js. 
1. Создайте папку для будущего приложения: 
	
	```
      mkdir lab5 
      cd lab5
    ```
1. Создайте конфигурационный файл.
    Он должен называться `package.json` и содержать в себе следующие строки:

    \lstinputlisting{../express/package.1.json}
    
    Обратите внимание на версию \code{express} в секции \code{dependencies:}
    желательно, во избежание сюрпризов в будущем, указывать конкретную версию
    фреймворка. На данный момент это  \code{4.0.0-rc2.} Актуальный
    номер версии в репозитории можно узнать с помощью команды

    \begin{lstlisting}
      # npm info express version
    \end{lstlisting}

  \end{item}
  \begin{item}

    Введите команду
    \begin{lstlisting}
      # npm install
    \end{lstlisting}

    После выполнения команды появится каталог \code{./node\_modules,}
    содержащий все зависимости проекта. Их также можно посмотреть с
    помощью команды \code{npm ls.}

  \end{item}
  \begin{item}

    Создайте главный файл приложения, например,\code{app.js}:

    \lstinputlisting{../express/app.1.js}

    и каталог с представлениями

    \begin{lstlisting}
      # mkdir views
    \end{lstlisting}
		
    А также папку для статических ресурсов, например, \texttt{public} 
		\begin{lstlisting}
      # mkdir public
    \end{lstlisting}
  \end{item}
  
  \begin{item}

    В предыдущем пункте мы указали \code{jade} в качестве
    шаблонизатора. Создайте представление для обработки формы:

    \code{views/form.jade:}
    \lstinputlisting{../express/views/form.jade}

    Строка \code{include form.html} добавляет файл формы в формате
    простого \code{html} в представление. При желании, вместо включения можно
    использовать более краткий \code{jade} для разметки.

    \code{views/form.html:}
    \lstinputlisting{../express/views/form.1.html}
    
  \end{item}
  \begin{item}
    Любуемся результатом
    \begin{lstlisting}
      # node app.js 
      # google-chrome "\url{http://localhost:3000/}"
    \end{lstlisting}
    
  \end{item}
  \begin{item}
    Добавим в приложение функцию поиска. Чаще всего в качестве БД для
    \code{Node.js} используется \code{mongoDB}. Порядок установки описан в предыдущих лабораторных.
  \end{item}
  \begin{item}
    Запускаем сервис mongodb, если еще не запущен.
  \end{item}
  \begin{item}
    Создадим базу данных для приложения.
    \begin{lstlisting}
      # mongo
    \end{lstlisting}
    Откроется интерактивный шелл доступа к БД. 
    \begin{lstlisting}
      > use hellodb
    \end{lstlisting}
    
  \end{item}
  \begin{item}
    Теперь мы в нашей новой базе. Но фактически база не будет создана,
    пока в нее не будут записаны никакие данные. Занесем туда парочку
    новых записей, создав попутно новую коллекцию \code{users}: 
    \begin{lstlisting}
      > u1 = {name: "ivan", surname: "petrov", description: "loves apples"}
      > u2 = {name: "vasya", surname: "ivanov", description: "hates dogs"}
      > db.users.insert(u1)
      > db.users.insert(u2)
      > db.users.find()
    \end{lstlisting}
    
  \end{item}
  \begin{item}
    Наше приложение будет искать описание людей по запросу.
    
    Воспользуемся фреймворком \code{mongoose} для извлечения данных из
    БД. Подправим зависимости:
    
    \code{package.json:}
    \lstinputlisting{../express/package.json}

    ... обновляемся:

    \begin{lstlisting}
      # npm install
    \end{lstlisting}

    ... подключаемся, добавляем схему, создаем модель, ищем данные по
    запросу и возвращаем:
    
    \code{app.js, с комментариями:}
    \begin{verbatim}
// подчключаем необходимые компоненты: фреймворк express
var express = require('express'),
    // модуль для управления путями
		path = require("path"),
    // компонент парсера HTML и JSON для него, 
    // подробнее: в туториале на сайте expressjs.com
    bodyParser = require('body-parser'),
    // библиотеку mongoose для более удобного
    // взаимодействия с БД
    mongoose = require('mongoose'),
    // и класс для создания схемы БД
    dbSchema = mongoose.Schema,
    app = express();

// соединияемся с сервером mongoDB
mongoose.connect('mongodb://localhost/hellodb');

// объявляем схему хранящихся в документе mongoDB
// данных. Таким образом, можно работать с nosql
// базой в привычном стиле
var usersSchema = new dbSchema({
  name:  String,
  surname: String,
  description:   String
});

// создаем модель по схеме, указывая на коллекцию 'users'
var usersModel = mongoose.model('users', usersSchema);

// указываем каталог с представлениями
app.set('views', __dirname + '/views');
// устанавливаем язык шаблонизатора
app.set('view engine','jade');
// используем body-parser для обработки запросов
app.use(bodyParser());

// Статические ресурсы будут размещены в папке public
// При обращении к этим файлам public указывать не надо
app.use(express.static(path.join(__dirname, 'public')));

// объявляем GET маршрут
app.get('/form', function(req, res) {
    // отдаем по запросу обработанное представление
    res.render('form', {
        // устанавливаем в представлении необходимые
        // переменные
		pageTitle: 'Ajax Form'
	});
});

// объявляем POST маршрут, для приема данных
app.post('/submit', function(req, res) {
    
    usersModel
    // ищем записи, соответствующие запросу
        .find({name: req.body.name, 
					surname: req.body.surname})
    // отправляем в ответ результат поиска
        .exec(function(err,docs) {
            res.send(docs);
        });

});

// запускаем сервер приложения на порту 3000
app.listen(3000);

\end{verbatim}
    ... и немного изменим страничку формы под новый формат данных:

\textbf{Дополнительное задание: }
\begin{itemize}
	\item Использовать возможности jQuery для отображения галерей, анимации и другого (на выбор).
\end{itemize}
