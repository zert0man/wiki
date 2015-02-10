# Лабораторная работа 2. PHP Silex

## Цели работы
- Познакомиться с языком PHP.
- Изучить реализацию паттерна MVC в микрофреймворке Silex.
- Изучить принципы шаблонизации на примере Twig.

## Краткие теоретические сведения

### Принцип работы HTTP-сервера

### Silex

**Silex** - MVC-микрофреймворк для разработки веб-приложений на языке PHP.

Объект `$app` представляет собой контейнер компонентов.

```
require_once __DIR__.'/../vendor/autoload.php'; 

$app = new Silex\Application(); 

$app->get('/hello/{name}', function($name) use($app) { 
    return 'Hello '.$app->escape($name); 
}); 

$app->run(); 
```

### Twig

### Doctrine

## Порядок выполнения
### Установка и настройка 
1. Скачать Silex и распаковать в папку, общую с vagrant-коробкой. 
1. Настроить виртуальный хост `1.mesdt` на сервере nginx. Проверить работоспособность. Сконфигурируйте перенаправление на `index.php`, используйте настройки для вашего веб-сервера ([http://silex.sensiolabs.org/doc/web_servers.html](http://silex.sensiolabs.org/doc/web_servers.html)).
- Для **nginx**. На виртуальной машине создать файл `/etc/nginx/sites-available/1.mesdt` по аналогии с файлом `0.mesdt`. Добавить конфигурацию из документации.
- Для **apache**.
1. Вся логика веб-приложения будет реализована в файле `/web/index.php`. Однако, кроме собственно html-страниц наш сервер должен отдавать браузеру css, js-скрипты и картинки. Это просто файлы, которые лежат в директории сайта. Все эти файлы называются статическими ресурсами сайта. Для того, чтобы браузер имел доступ к ним, добавим в начало `index.php` соответствующую проверку. Если пришедший от пользователя запрос содержит в url имя файла, то скрипт передает управление веб-серверу.
   
```
// Для php -S host:port -t web web/index.php, чтобы статика отдавалась
if (php_sapi_name() === 'cli-server' && is_file(__DIR__ . preg_replace('/(\?.*)$/', '', $_SERVER['REQUEST_URI']))) {
return false;
}
```

### Подключение к базе данных
1. Подключиться к базе данных с помощью Doctrine и вывести список объектов.
```
use Doctrine\DBAL\Connection;
use Silex\Provider\DoctrineServiceProvider;
```

```
use Silex\Application;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpKernel\Exception\NotFoundHttpException;
```
### Подключение шаблонов
1. Настроить вывод данных с помощью шаблонов Twig.
```
use Silex\Provider\TwigServiceProvider;
```


## Порядок защиты работы
При защите лабораторной работы необходимо предоставить работающее web-приложение, реализованное на фреймворке Silex и запущенное на web-сервере. Приложение должно выводить список объектов из базы данных.
Отчет должен содержать титульный лист, задание, код контроллера, код шаблонов Twig.

## Ссылки на документацию
- Документация по PHP [http://silex.sensiolabs.org/documentation](http://silex.sensiolabs.org/documentation)
- Документация по PHP на русском [http://silex.sensiolabs.org/documentation](http://silex.sensiolabs.org/documentation)
- Документация по Twig
- PHP Silex Docs [http://silex.sensiolabs.org/documentation](http://silex.sensiolabs.org/documentation)
- Конфигурирование сайта под Silex [http://silex.sensiolabs.org/doc/web_servers.html](http://silex.sensiolabs.org/doc/web_servers.html)