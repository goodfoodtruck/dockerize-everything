FROM php:8.3-fpm-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1

ENV APP_ENV=prod

RUN apk update && \
    apk add --no-cache \
        nginx \
        zip \
        git \
        unzip \
        icu-dev && \
    rm -rf /var/cache/apk/*

RUN docker-php-ext-install intl

COPY --from=composer:lts /usr/bin/composer /usr/bin/composer

COPY composer.* .

COPY . .

RUN composer install --no-dev --optimize-autoloader

RUN chown -R www-data:www-data /var/www/html

USER www-data

RUN php bin/console asset-map:compile

RUN php bin/console cache:clear --env=prod
