FROM php:7.1-fpm

RUN apt-get update --fix-missing

RUN apt-get install -y libssl-dev && pecl install mongodb && docker-php-ext-enable mongodb

RUN apt-get install -y zlib1g-dev libicu-dev g++ && docker-php-ext-configure intl && docker-php-ext-install intl

RUN docker-php-ext-install opcache

RUN docker-php-ext-install pdo_mysql

#Imagick
RUN apt-get install pkg-config libmagickwand-dev wget -y \
    && cd /tmp \
    && wget https://pecl.php.net/get/imagick-3.4.3.tgz \
    && tar xvzf imagick-3.4.3.tgz \
    && cd imagick-3.4.3 \
    && phpize \
    && ./configure \
    && make install \
    && rm -rf /tmp/imagick-3.4.3 \
    && docker-php-ext-enable imagick

RUN docker-php-ext-install exif && docker-php-ext-enable exif

RUN usermod -u 1000 www-data

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD files /