FROM php:7.4-fpm

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY php.ini /usr/local/etc/php/conf.d/php.ini

RUN apt update && apt install -y libzip-dev zip mc nano libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    && docker-php-ext-install pdo_mysql mysqli zip \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && pecl install xdebug && docker-php-ext-enable xdebug \
    && mkdir -p /var/www/html/ && chown www-data:www-data /var/www/html/

RUN curl "https://www.1c-bitrix.ru/download/files/scripts/bitrixsetup.php" --output /var/www/html/bitrixsetup.php

CMD ["php-fpm"]
