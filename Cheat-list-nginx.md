# Как создать новый виртуальный хост на nginx
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