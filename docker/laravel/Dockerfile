FROM php:8.1.11-apache

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
apt-get install -y git libonig-dev zlib1g-dev libpng-dev libzip-dev libwebp-dev libjpeg62-turbo-dev libmcrypt-dev libfreetype6-dev && \
docker-php-ext-install pdo pdo_mysql && \
docker-php-ext-install mysqli && docker-php-ext-enable mysqli && \
docker-php-ext-install mbstring && docker-php-ext-enable mbstring && \
pecl install xdebug-3.1.1 && \
docker-php-ext-configure gd && \
docker-php-ext-enable xdebug && docker-php-ext-install zip && \
docker-php-ext-enable zip && docker-php-ext-install gd && docker-php-ext-enable gd && \
docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp && \
docker-php-ext-install -j$(nproc) gd

COPY 000-default.conf /etc/apache2/sites-available/
COPY ./php.ini /usr/local/etc/php/php.ini

RUN a2enmod rewrite

WORKDIR /var/www/backpack

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf