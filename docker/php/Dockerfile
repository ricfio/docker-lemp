ARG PHP_VERSION=7.4.16
FROM php:$PHP_VERSION-fpm-alpine

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000

# INSTALL: bash, git, pdo_mysql
RUN apk add --no-cache bash git && \
    docker-php-ext-install pdo_mysql

# INSTALL: tzdata (set timezone)
ARG TZ=
RUN apk add --no-cache tzdata
ENV TZ=$TZ

# INSTALL: composer, symfony
COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=symfonycorp/cli /symfony /usr/bin/symfony

# CUSTOMIZE: .bashrc
RUN echo "export PS1='🐳 \[\033[1;36m\]\h \[\033[1;34m\]\W\[\033[0;35m\] \[\033[1;36m\]# \[\033[0m\]'" >> ~/.bashrc
