# Create server certificate

> generate rsa 2048bit PRIVATE KEY
openssl genrsa -out server.key 2048

> create Certificate Signing Request
openssl req -new -key server.key -out server.csr

> sign own csr by myself
openssl x509 -req -in server.csr -signkey server.key -out server.crt -days 3650

> pull nginx container image
docker pull nginx:stable-alpine

> get default config
docker run nginx:stable-alpine cat /etc/nginx/conf.d/default.conf

> edit config
```
server {
    listen       443 ssl;
    server_name  localhost;
    ssl on;
    ssl_certificate /etc/nginx/ssl/server.crt;
    ssl_certificate_key /etc/nginx/ssl/server.key;

    access_log  /var/log/nginx/ssl_access.log  main;
    error_log  /var/log/nginx/ssl_error.log warn;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
}

server {
    listen       80;
    server_name  localhost;

    access_log  /var/log/nginx/access.log  main;
    error_log  /var/log/nginx/error.log warn;

    location / {
        return 301 https://$host$request_uri;
    }
}
```
> prepare for volume mount
mkdir conf.d
mv default.conf conf.d
mkdir ssl
mv server.key server.crt ssl

> create docker-compose.yml
```
version: '3'
services:
  nginx:
    image: nginx:stable-alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - "./ssl:/etc/nginx/ssl"
      - "./conf.d:/etc/nginx/conf.d"
```
