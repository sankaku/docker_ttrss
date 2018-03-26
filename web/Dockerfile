FROM nginx:1.13.7
RUN mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.bak
ADD target/*.conf /etc/nginx/conf.d/
RUN groupmod -g 1000 nginx \
    && usermod -u 1000 nginx \
    && mkdir -p /var/run/php-fpm \
    && chown -R nginx:nginx /var/run/php-fpm

