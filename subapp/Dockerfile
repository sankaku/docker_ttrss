FROM php:7.2-fpm-alpine3.6

RUN apk update \
    && apk add wget shadow \
    && wget https://bitbucket.org/fivefilters/full-text-rss/get/b57a2b7eedf3.zip -O /tmp/fivefilters.zip \
    && unzip /tmp/fivefilters.zip -d /tmp/ \
    && mkdir -p /var/www/fivefilters \
    && mv /tmp/fivefilters-full-text-rss-b57a2b7eedf3/* /var/www/fivefilters/ \
    && rm -rf /tmp/fivefilters*

RUN useradd -s /sbin/nologin -u 1000 nginx \
    && mkdir -p /var/run/php-fpm \
    && chown -R nginx:nginx /var/run/php-fpm \
    && chown -R nginx:nginx /var/www/fivefilters

# PHP extentions
RUN apk update \
    && apk add build-base gcc autoconf libzip-dev \
    && pecl install zip \
    && yes "" | pecl install apcu \
    && docker-php-ext-enable zip apcu

# suppress PHP warnings(old fivefilters app with PHP7 displays many PHP warnings)
# i.e.) error_reporting(E_ALL ^ E_NOTICE) -> error_reporting(0)
RUN sed -i -r 's/(error_reporting)\([^\)]+\)/\1\(0\)/' /var/www/fivefilters/makefulltextfeed.php

# php-fpm setting
COPY ./target/www.conf /usr/local/etc/php-fpm.d/zzz-www.conf

