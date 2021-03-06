# Лабораторная работа 1. Знакомство с инструментарием
- [Цели работы](#Цели-работы)
- [Задание](#Задание)
- [Теоретическая информация](#Теоретическая-информация)
- [Инструменты](#Инструменты)
- [Порядок выполнения](#Порядок-выполнения)
- [Порядок защиты работы](#Порядок-защиты-работы)
- [Ссылки на скачивание инструментов](#Ссылки-на-скачивание-инструментов)
- [Ссылки на документацию](#Ссылки-на-документацию)
- [Дополнительная литература](#Дополнительная-литература)
- [Контрольные вопросы](#Контрольные-вопросы)

## Цели работы
- познакомиться с веб-сервером (nginx или Apache);
- познакомиться с шаблоном верстки HTML5 Twitter Bootstrap;
- познакомиться СУБД MySQL и средствами администрирования Adminer и PhpMyAdmin.	

## Задание
1. Установить виртуальную среду разработки для выполнения лабораторных работ на основе Vagrant или пакет серверов XAMPP.
2. Создать адаптивный html-шаблон для использования в последующих лабораторных работах.
3. Изучить инструменты администрирования для MySQL и создать базу данных для последующих лабораторных работ.

## Теоретическая информация

### HTTP-сервера
Разработка web-приложений основывается на клиент-серверной архитектуре. В качестве клиентского приложения выступает браузер, а в качестве сервера - либо специально разработанное ПО, либо (более распространенная ситуация) HTTP-сервер.

**HTTP-сервер** - это программа, которая обрабатывает GET и POST запросы по протоколу HTTP. Два наиболее распространенных HTTP-сервера - это Apache и Nginx. Оба сервера могут обрабатывать запросы к статическим ресурсам (страницам в формате html, файлам css, js и картинкам), а также имеют подключаемые модули, которые позволяют использовать скриптовые языки (такие как PHP, Python, Ruby и т.д.) и генерировать динамические html-страницы "на лету" в зависимости от запроса пользователя.

В большинстве случаев современные web-сервера - это не отдельные компьютеры, а виртуальные машины, предоставляемые на условия IaaS или PaaS. Зачастую настройки на реальном сервере существенно отличаются от настроек на локальной машине. Поэтому для разработки может быть использована специальная виртуальная машина с настройками реального сервера. Это позволяет унифицировать среду для всех разработчиков в пределах проекта и избежать проблем с совместимостью. Для выполнения лабораторных работ есть такая среда с настроенными серверами на основе Virtual Box и Vagrant. Однако, вы можете избрать другой путь, и устанавливать на своей машине сервера по мере необходимости.

### Немного о доступе к серверу 
Для доступа к веб-серверу используются, как правило, протоколы ftp (file transport protocol) и ssh. SSH - сетевой протокол прикладного уровня, позволяющий производить удалённое управление операционной системой и туннелирование TCP-соединений (например, для передачи файлов). Чтобы использовать ssh, необходимо установить специальную программу - ssh-клиент.

Для лабораторных работ на базе Vagrant рекомендуется использовать клиент, который идет в комплекте системы контроля версий Git. Это самая популярная система контроля версий для проектов с открытым кодом.

### Адаптивная верстка
Наиболее распространенным способом взаимодействия с пользователем в web являются html-страницы. Развитие мобильных устройств привело к тому, что от современных интернет-страниц требуется корректное отображение не только в разных браузерах, но и в очень большом диапазоне расширений экрана. Верстка, удовлетворяющая этому требованию, называется **отзывчивой**. Отзывчивая верстка - это компонент адаптивной, различия между этими понятиями вы можете найти в Википедии (см. список литературы). Такая верстка требует тщательного тестирования и учета множества нюансов. Производство сайтов - огромная индустрия, и создавать сложную адаптивную верстку с "нуля" невыгодно. В качестве основы для будущих интернет-страниц используются специальные html-фреймворки. Один из них - **Twitter Bootstrap**. Этот фреймворк состоит из одного css-файла (стили страницы) и нескольких js-файлов (скрипты) и обладает широкими возможностями: качественная адаптивная верстка на основе сетки (попробуйте изменить размер окна браузера на официальном сайте фреймворка), большое количество разнообразных элементов (формы, панели навигации, слайдеры, маркеры, всплывающие окна и многое другое). При создании страницы на основе этого фреймворка создается html-код (широкий спектр примеров находится на сайте фреймворка) и дополнительный файл css, который позволяет настроить верстку под конкретный дизайнерский макет.
Примеры сайтов можно посмотреть здесь: http://expo.getbootstrap.com/.

### СУБД MySQL
**MySQL** - свободная реляционная система управления базами данных. Разработку и поддержку MySQL осуществляет корпорация Oracle, получившая права на торговую марку вместе с поглощённой Sun Microsystems, которая ранее приобрела шведскую компанию MySQL AB. Продукт распространяется как под GNU General Public License, так и под собственной коммерческой лицензией.

Существует множество инструментов для администрирования MySQL, как платных, так и бесплатных. Наиболее распространенный среди них - **phpMyAdmin**, бесплатное php-приложение, которое, как правило, установлено на серверах интернет-провайдеров. Аналогом является приложение **Adminer**.

MySQL поддерживает несколько типов таблиц, что позволяет гибко настраивать базу в зависимости от соотношений операций чтения-записи, необходимого уровня скорости работы и надежности.

Рассмотрим два наиболее используемых типа таблиц. Другие типы таблиц вы можете изучить в документации (см. ссылку в списке литературы).

**MyISAM**

Данный тип таблиц предназначен для быстрого доступа к информации. Исторически - один из ранних типов таблиц в MySQL. Многие недостатки не позволяют использовать этот тип таблиц в больших проектах, но для блога, сайта-визитки и других маленьких и средних проектов, не требующих большого количества операций записи и не хранящих критическую информацию, данный вариант наиболее эффективен.  
- транзакций нет
- макс. размер на диске: 256Тб
- блокировка: вся таблица
- возможность полнотекстового индекса и быстрого поиска
- отсутствует поддержка целостности и внешних ключей
- поддержка репликации
- каждый столбец может иметь свою кодировку
- медленные операции записи (не подходит для высоконагруженных систем)
- невысокая надежность (не используйте для финансовых операций и делайте бэкапы!)

**InnoDB**

Один из наиболее быстрых и надежных современных движков для таблиц (не только в MySQL). Операции чтения работают значительно медленнее, чем в MyISAM, особенно если отсутствуют индексы.
- полная поддержка транзакций (4 уровня изоляции)
- макс. диск: 64Тб
- блокировка записи (не таблицы), два вида блокировок (SHARED, EXCLUSIVE)
- полнотекстовый индекс: нет
- индексы кластеризуются для «типичных запросов»
- поддержка целостности (внешние ключи)

## Инструменты
- Ваш любимый браузер (Google Chrome или Mozilla Firefox последней версии, не умничайте про IE).
- Virtual Box, Vagrant, ssh-клиент и виртуальная машина для выполнения лабораторных работ.
- СУБД MySQL в составе набора серверов, инструменты Adminer и PHP MyAdmin.
- Twitter Bootstrap.

## Порядок выполнения
### Установка виртуальной машины mesdt
Если по каким-то причинам у вас не получается, воспользуйтесь [страничкой помощи](Cheat-list-Vagrant), или альтернативным вариантом: поставьте [XAMPP](Install-XAMPP). 

1. Установить Virtual Box, если он еще не установлен. Проверить в настройках BIOS, разрешена ли виртуализация.
2. Установить Vagrant, если он еще не установлен. Для пользователей Windows: создайте переменную среды VAGRANT_HOME и пропишите в ней адрес пустого каталога, где Vagrant будет хранить свое глобальное состояние и образы виртуальных машин. Название должно быть латинскими буквами. Название папки для виртуальных машин тоже должно быть латинскими буквами. 
3. Для работы с консолью сервера установите ssh-клиент. Мы рекомендуем Git ssh. Чтобы на Windows заработала команда `vagrant ssh`, добавьте путь до ssh-клиента в переменную среды Path:  
`PATH=%PATH%;C:\Program Files (x86)\Git\bin`
4. Скачать и распаковать образ виртуальной машины.
5. Выполнить следующие команды:			
 
 ```
 vagrant box add --name mesdt mesdt.box
 vagrant init mesdt # команду выполнять в новой пустой директории
 ```
 
6. После выполнения этих команд в папке появится файл `Vagrantfile`. Настройте папку виртуальной машины на каталог вашей системе, который будет вам удобен, раскомментировав и исправив строчку
 
 ```
 config.vm.synced_folder "c:/vagrant/data", "/home/q/hws"
 ```
 
Здесь "/home/q/hws" - папка на виртуальной машине для выполнения лабораторных работ, "c:/vagrant/data" - любая пустая папка на вашем компьютере.
7. Запустите виртуальную машину:
 
 ```
 vagrant up
 vagrant ssh
 ```
 
8. В консоли сервера выполните команду `ifconfig` и узнайте ip-адрес сервера.
9. Для Windows-пользователей. Зайдите в папку `C:\Windows\System32\drivers\etc` и скопируйте оттуда файл hosts. Как правило, даже с администраторскими правами отредактировать его не удается. Поэтому надо скопировать в другую папку, отредактировать и вернуть на место. Добавьте в этот файл следующие строчки, заменив  `172.28.128.3` на ваш адрес сервера:

 ```
 # Лабораторные работы
 172.28.128.3    0.mesdt 
 172.28.128.3    1.mesdt 
 172.28.128.3    2.mesdt  
 172.28.128.3    3.mesdt  
 172.28.128.3    4.mesdt  
 172.28.128.3    5.mesdt 
 172.28.128.3    6.mesdt  
 172.28.128.3    7.mesdt 
 # Клон http://getbootstrap.com/ 
 172.28.128.3    twbs.mesdt  
 # Администраторы базы mysql
 172.28.128.3    adminer.mesdt  
 172.28.128.3    phpmyadmin.mesdt
 ```
10. Проверьте, что всё заработало, набрав адреса в браузере.

### Адаптивная верстка с использованием Twitter Bootstrap
1. Открыть задание, разработать макеты двух страниц в соответствии с заданием. Реализовать макеты с помощью Twitter Bootstrap. Требования к шаблону:
- шаблон должен состоять не менее чем из двух различных страниц;
- одна из страниц должна содержать список объектов в соответствии с заданием (на странице должны быть перечислены объекты и их основные характеристики); 
- вторая страница должна содержать полную информацию об одном объетке: название, характеристики, изображение и др.;
- страницы должны быть в формате html5, и в кодировке utf8;
- на страницах должны использоваться навигационные панели;
- на страницы должны быть элементы с различными фонами.
2. Сложите полученный результат в папку `/0` в каталоге, который вы сделали общей папкой с виртуальной машиной, зайдите в браузере на страницу `0.mesdt` и убедитесь, что всё работает. **Обратите внимание! Вы создаете шаблон, заготовку сайта! Загружать туда данные из базы не надо, это просто статические страницы.**	
		
### Разработка схемы базы данных и реализация схемы в MySQL		
1. С помощью любого CASE-средства или вручную разработать физическую модель базы данных для MySQL в соответствии с заданием (3-5 таблиц). 
2. Создать базу данных на сервере MySQL. Логин `root`, пароль `wut`. База данных должна поддерживать ссылочную целостность и русские символы. При создании базы используйте кодировку utf8.
3. С помощью PhpMyAdmin или Adminer внести на сервер несколько записей. 
4. Выполнить экспорт базы данных.

### Дополнительно		
В качестве дополнительного задания студент может:
- настроить другое доменное имя для сайта;
- использовать слайдер, модальные окна и другие дополнительные компоненты в страницах описания объектов.

## Порядок защиты работы
При защите лабораторной работы необходимо предоставить:
- шаблон верстки двух страниц в Twitter Bootstrap в соответствии с заданием; страницы должны быть доступны как сайт на виртуальном сервере;
- база данных на сервере MySQL, в соответствии с заданием; необходимо продемонстрировать умение пользоваться инструментом PhpMyAdmin и Adminer;
- отчет, содержащий титульный лист, задание, исходный код вёрстки, скриншоты верстки, структуру базы данных, код скрипта генерации базы данных.

## Ссылки на скачивание инструментов
- Virtual Box [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
- Vagrant [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)
- Виртуальная машина Mesdt ("sudo mc" убирает проблемы с доступом к файловой системе) [https://drive.google.com/file/d/0Bwl2Kb4AFw4ISFlYdnNHLUdua1k/view?usp=sharing](https://drive.google.com/file/d/0Bwl2Kb4AFw4ISFlYdnNHLUdua1k/view?usp=sharing) 
- Виртуальная машина Mesdt2 (лучше качать первую, исправлена проблема с правами доступа к каталогу hws, но появилась проблема с ключом для SSH) [https://drive.google.com/file/d/0Bwl2Kb4AFw4IQll4alZ4cVFtVWc/view?usp=sharing](https://drive.google.com/file/d/0Bwl2Kb4AFw4IQll4alZ4cVFtVWc/view?usp=sharing)
- Git [http://git-scm.com/downloads](http://git-scm.com/downloads)
- XAMPP [http://www.apachefriends.org/index.html](http://www.apachefriends.org/index.html)

## Ссылки на документацию
- Nginx [http://nginx.org/ru/](http://nginx.org/ru/)
- MySQL [www.mysql.com](www.mysql.com)
- Twitter Bootstrap [http://getbootstrap.com/](http://getbootstrap.com/), копия - [twbs.mesdt](twbs.mesdt)

## Дополнительная литература
- [Краткая справка по REST](https://ru.wikipedia.org/wiki/REST)
- [Статистика популярности веб-серверов.](http://news.netcraft.com/archives/2015/01/15/january-2015-web-server-survey.html)
- [Адаптивный веб-дизайн](https://ru.wikipedia.org/wiki/%D0%90%D0%B4%D0%B0%D0%BF%D1%82%D0%B8%D0%B2%D0%BD%D1%8B%D0%B9_%D0%B2%D0%B5%D0%B1-%D0%B4%D0%B8%D0%B7%D0%B0%D0%B9%D0%BD)

## Контрольные вопросы
1. Что такое веб-сервер?
2. Что такое REST?
3. Что такое PaaS и IaaS?
4. Что такое адаптивная верстка?
5. MySQL. Особенности, типы таблиц.
6. Что такое репликация?