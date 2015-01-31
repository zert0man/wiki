# Лабораторная работа 1. Знакомство с инструментарием

## Цели работы
- познакомиться с сервером Apache;
- познакомиться с шаблоном верстки HTML5;
- познакомиться СУБД MySQL и средствами администрирования Adminer и PhpMyAdmin.	

## Задание

## Теоретическая информация
Сервера. Виртуализация. Virtual Box. Vagrant. ssh. Git
Apache MySQL Adminer PhpMyAdmin TwitterBootstrap

## Системные требования к компьютеру

## Порядок выполнения
1. Установить Virtual Box, если он еще не установлен. Проверить в настройках BIOS, разрешена ли виртуализация.
1. Установить Vagrant, если он еще не установлен. Для пользователей Windows: создайте переменную среды VAGRANT_HOME и пропишите в ней адрес пустого каталога, где Vagrant будет хранить свое глобальное состояние и образы виртуальных машин. Название должно быть латинскими буквами. Название папки для виртуальных машин тоже должно быть латинскими буквами. 
1. Для работы с консолью сервера установите ssh-клиент. Мы рекомендуем Git ssh. Чтобы на Windows заработала команда `vagrant ssh`, добавьте путь до ssh-клиента в переменную среды Path:  
`PATH=%PATH%;C:\Program Files (x86)\Git\bin`
1. Скачать и распаковать образ виртуальной машины.
1. Выполнить следующие команды:			
`vagrant box add --name mesdt mesdt.box
vagrant init mesdt # команду выполнять в новой пустой директории
vagrant up
vagrant ssh`
1. В консоли сервера выполните команду `ifconfig` и узнайте ip-адрес сервера.
1. Для Windows-пользователей. Зайдите в папку `C:\Windows\System32\drivers\etc` и скопируйте оттуда файл hosts. Как правило, даже с администраторскими правами отредактировать его не удается. Поэтому надо скопировать в другую папку, отредактировать и вернуть на место. Добавьте в этот файл следующие строчки, заменив  `172.28.128.3` на ваш адрес сервера:

```
# Лабораторные работы
172.28.128.3    www.0.mesdt
172.28.128.3    www.1.mesdt
172.28.128.3    www.2.mesdt  
172.28.128.3    www.3.mesdt  
172.28.128.3    www.4.mesdt  
172.28.128.3    www.5.mesdt 
172.28.128.3    www.6.mesdt  
172.28.128.3    www.7.mesdt  
172.28.128.3    0.mesdt 
172.28.128.3    1.mesdt 
172.28.128.3    2.mesdt  
172.28.128.3    3.mesdt  
172.28.128.3    4.mesdt  
172.28.128.3    5.mesdt 
172.28.128.3    6.mesdt  
172.28.128.3    7.mesdt 
# Клон http://getbootstrap.com/
172.28.128.3    www.twbs.mesdt  
172.28.128.3    twbs.mesdt  
# Администраторы базы mysql
172.28.128.3    www.adminer.mesdt  
172.28.128.3    adminer.mesdt  
172.28.128.3    www.phpmyadmin.mesdt 
172.28.128.3    phpmyadmin.mesdt
```

1.

## Ссылки на скачивание инструментов
- Virtual Box [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
- Vagrant [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)
- Виртуальная машина Mesdt [http://brn22.tk/mesdt.box](http://brn22.tk/mesdt.box) 
- Twitter Bootstrap [http://getbootstrap.com/](http://getbootstrap.com/)

## Ссылки на документацию

## Контрольные вопросы
1.
1.