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
1. Скачать Silex и распаковать в папку, общую с vagrant-коробкой.
1. Настроить виртуальный хост `1.mesdt` на сервере nginx. Проверить работоспособность.
На виртуальной машине создать файл `/etc/nginx/sites-available/1.mesdt`
1. Подключиться к базе данных с помощью Doctrine и вывести список объектов.
1. Настроить вывод данных с помощью шаблонов Twig.
1.

## Порядок защиты работы
При защите лабораторной работы необходимо предоставить работающее web-приложение, реализованное на фреймворке Silex и запущенное на web-сервере. Приложение должно выводить список объектов из базы данных.
Отчет должен содержать титульный лист, задание, код контроллера, код шаблонов Twig.

## Ссылки на документацию
- Документация по PHP [http://silex.sensiolabs.org/documentation](http://silex.sensiolabs.org/documentation)
- Документация по PHP на русском [http://silex.sensiolabs.org/documentation](http://silex.sensiolabs.org/documentation)
- Документация по Twig
- PHP Silex Docs [http://silex.sensiolabs.org/documentation](http://silex.sensiolabs.org/documentation)