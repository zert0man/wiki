#Cheat list Twig
## How to
### Вставка значения из контроллера
Вывести значение параметра `foo1`
```
{{ foo1 }}
```
Вывести значение из массива `foo` по ключу `bar`. Варианты эквивалентны.
```
{{ foo2.bar }}
{{ foo2['bar'] }}
```
### Вставка блока и пример наследования
Базовый шаблон `base.html`:
```
<!DOCTYPE html>
<html>
    <head>
        {% block head %}
            <link rel="stylesheet" href="style.css" />
            <title>{% block title %}{% endblock %} - My Webpage</title>
        {% endblock %}
    </head>
    <body>
        <div id="content">{% block content %}{% endblock %}</div>
        <div id="footer">
            {% block footer %}
                &copy; Copyright 2011 by <a href="http://domain.invalid/">you</a>.
            {% endblock %}
        </div>
    </body>
</html>
```
Шаблон наследник, переопределяет блоки, остальное остается на месте;
```
{% extends "base.html" %}

{% block title %}Index{% endblock %}
{% block head %}
    {{ parent() }}
    <style type="text/css">
        .important { color: #336699; }
    </style>
{% endblock %}
{% block content %}
    <h1>Index</h1>
    <p class="important">
        Welcome to my awesome homepage.
    </p>
{% endblock %}
```

### Условия
```
{% if kenny.sick %}
    Kenny is sick.
{% elseif kenny.dead %}
    You killed Kenny! You bastard!!!
{% else %}
    Kenny looks okay --- so far
{% endif %}

{% if users|length > 10 %}
    ...
{% endif %}
```
### Циклы
```
        {% for item in navigation %}
            <li><a href="{{ item.href }}">{{ item.caption }}</a></li>
        {% endfor %}
```
## Сслыка на документацию
[http://twig.sensiolabs.org/documentation](http://twig.sensiolabs.org/documentation)