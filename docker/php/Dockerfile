ARG PHP_VERSION=7.4.16
FROM php:$PHP_VERSION-fpm-alpine

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000 9003

# INSTALL: bash, git, tzdata
RUN apk add --no-cache \
    bash \
    git \
    tzdata \
    gettext

# INSTALL: Xdebug
ARG XDEBUG_MODE=off
ARG XDEBUG_CLIENT_PORT=9003
ARG XDEBUG_CLIENT_HOST=host.docker.internal
COPY conf.d/docker-php-ext-xdebug.ini.template /usr/local/etc/php/conf.d/
RUN apk --no-cache add $PHPIZE_DEPS && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    export XDEBUG_MODE=$XDEBUG_MODE && \
    export XDEBUG_CLIENT_PORT=$XDEBUG_CLIENT_PORT && \
    export XDEBUG_CLIENT_HOST=$XDEBUG_CLIENT_HOST && \
    envsubst < /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini.template > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    rm -f /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini.template

# INSTALL: composer, symfony
COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=symfonycorp/cli /symfony /usr/bin/symfony

# CUSTOMIZE: timezone
ARG PHP_SYSTEM_TZ=Europe/London
ENV TZ=$PHP_SYSTEM_TZ

# CUSTOMIZE: .bashrc
RUN echo "export PS1='🐳 [\[\033[1;36m\]\u@\h\[\033[0m\] \[\033[1;34m\]\W\[\033[0m\]]\\$ '" >> ~/.bashrc

SHELL ["/bin/bash"]
