# Cheat list nginx

Сервер nginx конфигурируется специальными файлами. На виртуальной машине они расположены в каталоге ``.
После внесения изменений в конфигурацию, чтобы она вступила в силу, сервер nginx необходимо перезагрузить командой:
 
```
nginx -s reload
```

Перезапускать остальные сервера и всю виртуальную машину не нужно.

## Пример виртуального хоста для Silex на nginx

```
server {
	listen 80;
	server_name 1.mesdt;
	root /home/q/hws/1/web;
	
	location = / {
		try_files @site @site;
	}

	location / {
		try_files $uri $uri/ @site;
	}

	location ~ \.php$ {
		return 404;
	}

        location @site {
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                include fastcgi_params;
		fastcgi_param SCRIPT_FILENAME $document_root/index.php;
        }
}

```

## Сслыка на документацию
[Руководство для начинающих](http://nginx.org/ru/docs/beginners_guide.html)
