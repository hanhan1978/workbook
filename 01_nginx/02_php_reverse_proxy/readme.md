
> pull nginx container image

docker pull nginx:stable-alpine

> pull PHP container image

docker pull php:7.2-fpm-alpine

> ceate htdocs

mkdir htdocs

> create index.php

vi htdocs/index.php
```
<?php
phpinfo();
```

> create static.html

vi htdocs/static.html
```
this is static html
```

> get default config

docker run nginx:stable-alpine cat /etc/nginx/conf.d/default.conf

> edit config

```
server {
    listen       80;
    server_name  localhost;

    access_log  /var/log/nginx/access.log  main;
    error_log  /var/log/nginx/error.log warn;

    location / {
        root   /usr/share/nginx/html;
        index  index.php index.html index.htm;
    }
    location ~ \.php$ {
        root   /usr/share/nginx/html;
        fastcgi_pass   php:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```
> prepare for volume mount
mkdir conf.d
mv default.conf conf.d

> create docker-compose.yml
```
version: '3'
services:
  nginx:
    image: nginx:stable-alpine
    ports:
      - "80:80"
    volumes:
      - "./conf.d:/etc/nginx/conf.d"
      - "./html:/usr/share/nginx/html"
    networks:
      - local

  php:
    image: php:7.2-fpm-alpine
    volumes:
      - "./html:/usr/share/nginx/html"
    networks:
      - local
networks:
  local:
    external:true
```

> check redirection
curl http://localhost
curl http://localhost/static.html
