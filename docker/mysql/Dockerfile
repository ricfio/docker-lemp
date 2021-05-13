FROM mariadb:latest

WORKDIR /var/lib/mysql

CMD ["mysqld"]

EXPOSE 3306

# CUSTOMIZE: .bashrc, .my.cnf
ARG MYSQL_DATABASE
ARG MYSQL_ROOT_PASSWORD
RUN echo "export PS1='🐳 [\[\033[1;36m\]\h \[\033[1;34m\]\W\[\033[0m\]]\[\033[1;36m\]# \[\033[0m\]'" >> ~/.bashrc
RUN echo "[mysql]\ndatabase=$MYSQL_DATABASE\nuser=root\npassword=$MYSQL_ROOT_PASSWORD\n" >> ~/.my.cnf && chmod 0600 ~/.my.cnf
