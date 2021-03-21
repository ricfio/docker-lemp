FROM php:fpm-alpine

WORKDIR /var/www

RUN apk --update --no-cache add git bash && docker-php-ext-install pdo_mysql

COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY --from=symfonycorp/cli /symfony /usr/bin/symfony

CMD ["php-fpm"]

EXPOSE 9000
