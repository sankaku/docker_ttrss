FROM php:7.2.0-fpm-alpine3.6

# RUN apk update \
#     && apk add git shadow \
#     && git clone --progress --verbose https://tt-rss.org/git/tt-rss.git /var/www/ttrss

RUN apk update \
    && apk add shadow \
    && mkdir -p /var/www
COPY ./target/tt-rss /var/www/ttrss

RUN groupadd -g 1000 nginx \
    && useradd -s /sbin/nologin -u 1000 -g nginx nginx \
    && mkdir -p /var/run/php-fpm \
    && chown -R nginx:nginx /var/run/php-fpm \
    && chown -R nginx:nginx /var/www/ttrss
# RUN useradd -s /sbin/nologin -u 1000 nginx \
#     && chown -R nginx:nginx /var/www/ttrss

# to execute update.php
RUN cd /var/www/ttrss \
    && chmod -R 777 cache/images cache/upload cache/export cache/js feed-icons lock

# PHP extentions
RUN apk update \
    && apk add icu-dev \
    && docker-php-ext-install intl pdo_mysql mysqli

# php-fpm config
COPY ./target/www.conf /usr/local/etc/php-fpm.d/zzz-www.conf

