# FROM php:7.2.0-fpm-alpine3.6
# FROM php:5.6.32-fpm-alpine3.4
FROM php:5.6.32-fpm-jessie

# alpine version
# RUN apk update \
#     && apk add wget shadow \
#     && wget https://bitbucket.org/fivefilters/full-text-rss/get/b57a2b7eedf3.zip -O /tmp/fivefilters.zip \
#     && unzip /tmp/fivefilters.zip -d /tmp/ \
#     && mkdir -p /var/www/fivefilters \
#     && mv /tmp/fivefilters-full-text-rss-b57a2b7eedf3/* /var/www/fivefilters/ \
#     && rm -rf /tmp/fivefilters*

# debian version
RUN apt-get update \
    && apt-get install -y wget unzip \
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
# alpine version
# RUN apk update \
#     && apk add build-base gcc autoconf libzip libzip-dev \
#     && pecl install zip-1.15.2 \
#     && yes "" | pecl install apcu \
#     && docker-php-ext-enable zip apcu

# debian version
RUN apt-get update \
    && apt-get install -y gcc autoconf libzip-dev \
    && pecl install zip-1.15.2 \
    && docker-php-ext-enable zip

COPY ./target/www.conf /usr/local/etc/php-fpm.d/zzz-www.conf

