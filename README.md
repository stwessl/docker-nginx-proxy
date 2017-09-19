# docker-nginx-proxy
Docker Compose solution to run a nginx proxy for docker instances on site (Meant for development)
## How to use
This instance needs an network instance of blah to run so please create the network with
```
docker network create nginx-proxy
```
## How to connect other instances to run with this proxy

Add the following to any apache services in your docker-compose.yml
```
expose:
      - 80
environment:
    - VIRTUAL_HOST=dev.angama.co.za
    restart: always

```

eg. an xampp instance would look something like this
```
version: '2'
services:
  apache:
    expose:
      - 80
    image: tomsik68/xampp
    restart: always
    volumes:
      - .:/opt/lampp/htdocs
      - ./docker/apache/httpd.conf:/opt/lampp/etc/httpd.conf
      - ./docker/apache/httpd-vhosts.conf:/opt/lampp/etc/extra/httpd-vhosts.conf

    environment:
    - VIRTUAL_HOST=dev.angama.co.za
    restart: always
```