# Docker LEMP
## Docker Containers for Web Development on LEMP stack
LEMP is an environment built with [Docker](https://www.docker.com/) and oriented to Web development on LEMP stack.  

The term LEMP is an acronym that represents the environment configuration, based on:  
- [**L**inux](https://www.linux.it/) as Operating System  
- [**E**ngine-X](https://www.nginx.com/) as Web Server  
- [**M**ySQL](https://www.mysql.com/) database to store data  
- [**P**HP](https://www.php.net/) to process dynamic content  

The environment uses the following Docker Containers availables in [Docker Hub](https://hub.docker.com/):  
- [Alpine](https://alpinelinux.org/) (Docker Hub: [alpine:latest](https://hub.docker.com/_/alpine))
- [NGINX](https://www.nginx.com/) (Docker Hub: [nginx:alpine](https://hub.docker.com/_/nginx))
- [MariaDB](https://mariadb.org/) (Docker Hub: [mariadb:latest](https://hub.docker.com/_/mariadb))
- [PHP](https://www.php.net/) (Docker Hub: [php:fpm-alpine](https://hub.docker.com/_/php))

## Software and Tools
The solution includes also extra software and tools:  
- [Git](https://https://git-scm.com/)
- [Composer](https://getcomposer.org/)
- [Symphony](https://symfony.com/)

# Setup

## Requirements
Docker installed on the operating system:  
- [Docker Engine for Linux](https://hub.docker.com/search?q=&type=edition&offering=community&operating_system=linux)  
- [Docker Desktop for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)  
- [Docker Desktop for Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)  

## Install, Configuration and Build
Clone LEMP from the repository into your app folder:  
`git clone https://github.com/ricfio/docker-lemp.git app`  

Move in the app (docker-lemp) folder:  
`cd app`  

You can customize the configuration changing some variables in the .env file:  

|  Key                | Current value | Description         | Notes         |
|---------------------|:-------------:|---------------------|-------------------------------------------------------------------------|
| APP_NAME            | app           | Application name    |                                                                         |
| HTTP_PORT           | 8080          | HTTP port           |                                                                         |
| HTTPS_PORT          | 8443          | HTTPS port          |                                                                         |
| MYSQL_PORT          | 3306          | MySQL port          |                                                                         |
| MYSQL_USER          | user          | MySQL user          |                                                                         |
| MYSQL_PASSWORD      | user          | MySQL password      |                                                                         |
| MYSQL_ROOT_PASSWORD | root          | MySQL root password |                                                                         |
| PHP_VERSION         | 7.4.16        | PHP version         | [Docker Image](https://hub.docker.com/_/php): {$PHP_VERSION}-fpm-alpine |
| TZ                  | Europe/Rome   | TimeZone            |                                                                         |

Build the Docker Containers:  
`docker-compose build`  

`docker image ls lemp_*`  
```
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
lemp_linux   latest    5ed7e578a353   7 minutes ago   46MB
lemp_nginx   latest    6effdfc67af3   3 days ago      22.6MB
lemp_mysql   latest    19279c96333c   3 days ago      401MB
lemp_php     latest    93ac44225405   21 hours ago    122MB
```

Start all services (in background mode):  
`docker-compose up -d`  
```
Creating network "app" with the default driver
Creating app_linux ... done
Creating app_nginx ... done
Creating app_mysql ... done
Creating app_php   ... done
```

List all services running:  
`docker container ls --all -f NAME=app_*`  
```
CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                                         NAMES
ebdf2c240848   lemp_linux   "bash"                   30 seconds ago   Up 30 seconds                                                 app_linux
775dd4387a8e   lemp_nginx   "/docker-entrypoint.…"   30 seconds ago   Up 30 seconds   0.0.0.0:8080->80/tcp, 0.0.0.0:8443->443/tcp   app_nginx
24d77f6138b3   lemp_mysql   "docker-entrypoint.s…"   30 seconds ago   Up 30 seconds   0.0.0.0:3306->3306/tcp                        app_mysql
6763b26b9e20   lemp_php     "docker-php-entrypoi…"   30 seconds ago   Up 30 seconds   9000/tcp                                      app_php
```

Start all services with logs on console (CTRC+C to stop all services):  
`docker-compose up`  

Stop and Remove all containers:  
`docker-compose down`  
```
Stopping app_nginx ... done
Stopping app_php   ... done
Stopping app_mysql ... done
Stopping app_linux ... done
Removing app_nginx ... done
Removing app_php   ... done
Removing app_mysql ... done
Removing app_linux ... done
Removing network app
```

## Test the installation
Open the web browser and go to:  
- [http://localhost:8080](http://localhost:8080/)  

You should be see the output of a a phpinfo() script.  
```
<?php phpinfo() ?>
```

# Usage

## Folders

| Path         | Description   |
|--------------|---------------|
| ./docker     | Docker Files  |
| ./log        | Services Log  |
| ./opt        | Shared folder |
| ./www/public | Document Root |

So, you can:  
* check the logs from container services  
* add your files shared with all containers  
* working on your app files in the document root  

## Commands
open bash on linux container for commands execution:  
`docker exec -it app_linux bash`  
```
🐳 app_linux ~ # exit
```

exec commands on linux container:  
```
docker exec -it app_linux bash -c 'cat /etc/os-release'
docker exec -it app_linux bash -c 'bash --version'
docker exec -it app_linux bash -c 'git --version'
```

open bash on app_mysql container for commands execution:  
`docker exec -it app_mysql bash`  
```
🐳 app_mysql mysql # mysql --version
mysql  Ver 15.1 Distrib 10.5.9-MariaDB, for debian-linux-gnu (x86_64) using readline 5.2
```

open mysql console on app_mysql container (no password required):  
`docker exec -it app_mysql mysql`  
```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 5
Server version: 10.5.9-MariaDB-1:10.5.9+maria~focal mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [app]>
```

open bash on app_php container for commands execution:  
`docker exec -it app_php bash`  
```
🐳 app_php www # php -v
PHP 8.0.3 (cli) (built: Mar  6 2021 03:38:04) ( NTS )
Copyright (c) The PHP Group
Zend Engine v4.0.3, Copyright (c) Zend Technologies

🐳 app_php www # composer -V
Composer version 2.0.11 2021-02-24 14:57:23

🐳 app_php www # symfony -V
Symfony CLI version v4.23.2 (2021-03-02T17:16:03+0000 - stable)
```
