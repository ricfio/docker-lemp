FROM php:fpm-alpine

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000

# INSTALL: bash, git, pdo_mysql
#RUN apk --update --no-cache
RUN apk add --no-cache bash git && docker-php-ext-install pdo_mysql

# INSTALL: composer, symfony
COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=symfonycorp/cli /symfony /usr/bin/symfony

# CUSTOMIZE: .bashrc
RUN echo "export PS1='🐳 \[\033[1;36m\]\h \[\033[1;34m\]\W\[\033[0;35m\] \[\033[1;36m\]# \[\033[0m\]'" >> ~/.bashrc
