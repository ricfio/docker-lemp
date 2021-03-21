# Docker LEMP
## Docker Containers for Web Development on LEMP stack
LEMP is an environment built with [Docker](https://www.docker.com/) and oriented to Web development on LEMP stack.  

The term LEMP is an acronym that represents the environment configuration, based on:  
- **L**inux as Operating System  
- **E**ngine-X ([NGINX](https://www.nginx.com/)) as Web Server  
- [**M**ySQL](https://www.mysql.com/) database to store data  
- [**P**HP](https://www.php.net/) to process dynamic content  

The environment uses the following Docker Containers availables in [Docker Hub](https://hub.docker.com/):  
- [nginx:alpine](https://hub.docker.com/_/nginx)
- [mariadb:latest](https://hub.docker.com/_/mariadb)
- [php:fpm-alpine](https://hub.docker.com/_/php)

## Software and Tools
The solution includes also extra software and tools:  
- [Composer](https://getcomposer.org/)
- [Symphony](https://symfony.com/)

# Setup

## Requirements
Docker installed on the operating system:  
- [Docker Engine for Linux](https://hub.docker.com/search?q=&type=edition&offering=community&operating_system=linux)  
- [Docker Desktop for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)  
- [Docker Desktop for Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)  

## Install, Configuration and Build
Clone LEMP from the repository:  
`git clone https://github.com/ricfio/docker-lemp.git`  

You can customize the configuration changing the .env file.  
For example, you could change the http/s and mysql port or the mysql login information.  

`vi docker-lemp/.env`  

Build and Start the Docker Containers:  
`cd docker-lemp/docker`  
`docker-compose up`  

## Test the installation
Open the web browser and go to:  
- [http://localhost:8080](http://localhost:8080/)  

You should be see the output of a a phpinfo() script.  
```
<?php phpinfo() ?>
```

# Usage

You can add your files in the document root and check the logs:  

```
# Document Root:
./www/public/

# NGINX Logs:
./log/nginx/

# MySQL DataDir:
./docker/mysql/data/
```

## Commands
bash:  
`docker-compose run --rm php-fpm bash`  
```
bash-5.1# 
```

Composer:  
`docker-compose run --rm php-fpm composer -V`  
```
Composer version 2.0.11 2021-02-24 14:57:23
```

Symfony CLI:  
`docker-compose run --rm php-fpm symfony -V`  
```
Symfony CLI version v4.23.2 (2021-03-02T17:16:03+0000 - stable)
```
