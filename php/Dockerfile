FROM php:7.3.3-apache

ENV http_proxy http://proxy.example.com:8080
ENV https_proxy https://proxy.example.com:8080
ENV PHP_MEMCACHED_VERSION 3.1.3

COPY php.ini /usr/local/etc/php/

RUN apt-get update
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev \
  && docker-php-ext-install pdo_mysql mysqli mbstring gd iconv
RUN docker-php-ext-install opcache

RUN apt-get install -y apache2
ADD hoge.conf /etc/apache2/sites-available/hoge.conf
RUN cd /etc/apache2/sites-available/ && a2ensite hoge.conf && a2dissite 000-default.conf

RUN apt-get install -y libmemcached-dev zlib1g-dev
RUN curl -L -o /tmp/memcached.tar.gz https://github.com/php-memcached-dev/php-memcached/archive/v$PHP_MEMCACHED_VERSION.tar.gz \
    && tar xfz /tmp/memcached.tar.gz \
    && rm -r /tmp/memcached.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv php-memcached-$PHP_MEMCACHED_VERSION /usr/src/php/ext/memcached \
    && echo memcached >> /usr/src/php-available-exts \
    && docker-php-ext-install memcached

RUN { \
  echo 'session.save_handler = memcached'; \
  echo 'session.save_path = memacched:1121'; \
} >> /usr/local/etc/php/conf.d/docker-php-ext-memcached.ini

