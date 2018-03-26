# docker-ttrss

## update feeds
```sh
# useradd -s /bin/nologin cronuser
# echo '*/30 * * * * /usr/local/bin/php /var/www/ttrss/update.php --feeds --quiet' > /var/spool/cron/crontabs/cronuser
# chmod 600 /var/spool/cron/crontabs/cronuser
# chown cronuser:cronuser /var/spool/cron/crontabs/cronuser
# crond
```

