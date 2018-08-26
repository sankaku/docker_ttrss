FROM nginx:1.13
RUN mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.bak
RUN groupmod -g 1000 nginx \
    && usermod -u 1000 nginx \
    && mkdir -p /var/run/php-fpm \
    && chown -R nginx:nginx /var/run/php-fpm

# Password File for Basic Authentication
COPY target/.htpasswd /etc/nginx/.htpasswd
RUN chmod 400 /etc/nginx/.htpasswd \
    && chown nginx:nginx /etc/nginx/.htpasswd
