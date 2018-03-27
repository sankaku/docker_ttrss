FROM php:7.2-fpm-alpine3.6

RUN apk update \
    && apk add git shadow \
    && git clone --progress --verbose https://tt-rss.org/git/tt-rss.git /var/www/ttrss

# RUN apk update \
#     && apk add wget shadow \
#     && wget https://git.tt-rss.org/fox/tt-rss/archive/17.4.tar.gz -P /tmp \
#     && tar zxfv /tmp/17.4.tar.gz -C /var/www \
#     && mv /var/www/tt-rss /var/www/ttrss

RUN groupadd -g 1000 nginx \
    && useradd -s /sbin/nologin -u 1000 -g nginx nginx \
    && mkdir -p /var/run/php-fpm \
    && chown -R nginx:nginx /var/run/php-fpm \
    && chown -R nginx:nginx /var/www/ttrss

# to execute update_daemon2.php
RUN cd /var/www/ttrss \
    && chmod -R 777 cache/images cache/upload cache/export cache/js feed-icons lock \
    && docker-php-ext-install pcntl \
    && ln -s /usr/local/bin/php /usr/bin/php

# PHP extentions
RUN apk update \
    && apk add icu-dev \
    && docker-php-ext-install intl pdo_mysql mysqli

# php-fpm config
COPY ./target/www.conf /usr/local/etc/php-fpm.d/zzz-www.conf

# supervisord
RUN apk update \
    && apk add supervisor \
    && mkdir /var/log/supervisor
COPY target/supervisord.conf /etc/supervisord.conf
RUN chown nginx:nginx /etc/supervisord.conf \
    && chmod 400 /etc/supervisord.conf

CMD supervisord -c /etc/supervisord.conf
