FROM php:8.3

WORKDIR /var/www/html

COPY . /var/www/html

ENV COMPOSER_ALLOW_SUPERUSER=1

ENV APP_ENV=prod

RUN apt-get update && apt-get install -y \
    zip \
    git \
    unzip \
    libicu-dev\
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install intl

RUN curl -sS https://getcomposer.org/installer | php -- \
     --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash

RUN find / -type f -name symfony -exec mv {} usr/local/bin/symfony \; || true


RUN chown -R www-data:www-data /var/www
USER www-data

RUN composer install --no-dev --optimize-autoloader

USER root

RUN composer require symfony/runtime

RUN php bin/console asset-map:compile

RUN php bin/console cache:clear --env=prod

COPY .docker/nginx/grilli.com.conf /etc/nginx/sites-available/

RUN ln -s /etc/nginx/sites-available/grilli.com.conf /etc/nginx/sites-enabled/

CMD ["nginx","-g","daemon off;"]
# CMD ["sh", "-c", "symfony server:start --port=8000 --no-tls & nginx -g 'daemon off;'"]
