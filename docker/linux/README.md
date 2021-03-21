# Docker Container Linux

## Setup

Build the Docker Image:  
`docker build -t linux-test .`  

Run a temporary Docker Container:  
`docker run -it --rm -h linux-temp linux-test`  

Create and Start the Docker Container:  
`docker create -it --name linux-test -h linux-test linux-test`  
`docker start linux-test`  

Run the Docker Container (alternative to do Create and Start):  
`docker run -it -d --name linux-test -h linux-test linux-test`  

Stop the Docker Container:  
`docker stop linux-test`  

## Usage

You can login (bash) more and more time in the Docker Container:  
`docker exec -it linux-test bash`  
```
🐳 linux-test ~ #
```

linux version:  
`docker exec -it linux-test bash -c 'cat /etc/os-release'`  
```
NAME="Alpine Linux"
ID=alpine
VERSION_ID=3.13.2
PRETTY_NAME="Alpine Linux v3.13"
HOME_URL="https://alpinelinux.org/"
BUG_REPORT_URL="https://bugs.alpinelinux.org/"
```

bash version:  
`docker exec -it linux-test bash --version`  
```
GNU bash, version 5.1.0(1)-release (x86_64-alpine-linux-musl)
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```
