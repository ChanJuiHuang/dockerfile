FROM php:7.4-fpm

ARG APP_ENV=production

RUN apt-get update && apt-get install -y wget \
    cron \
    libpq-dev \
    libzip-dev \
    libpng-dev \
    libonig-dev \
    libzstd-dev \
    libssl-dev

RUN docker-php-ext-install --ini-name pdo_mysql.ini pdo_mysql && \
    docker-php-ext-install --ini-name pgsql.ini pgsql && \
    docker-php-ext-install --ini-name pdo_pgsql.ini pdo_pgsql && \
    docker-php-ext-install --ini-name sockets.ini sockets && \
    docker-php-ext-install --ini-name pcntl.ini pcntl && \
    docker-php-ext-install --ini-name opcache.ini opcache

RUN pecl install igbinary msgpack && \
    echo extension=igbinary.so > /usr/local/etc/php/conf.d/igbinary.ini && \
    echo extension=msgpack.so > /usr/local/etc/php/conf.d/msgpack.ini

RUN pecl bundle -d /usr/src/php/ext redis \
    && docker-php-ext-configure redis --enable-redis-igbinary --enable-redis-msgpack --enable-redis-lzf \
    && docker-php-ext-install --ini-name redis.ini redis

COPY ./composer-installer.sh /root
RUN chmod a+x /root/composer-installer.sh && bash -c /root/composer-installer.sh

COPY ./php-ini/php.ini-production /usr/local/etc/php/php.ini-production
COPY ./php-ini/php.ini-development /usr/local/etc/php/php.ini-development
RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini

COPY ./php-ini/conf.d/* /usr/local/etc/php/conf.d/
RUN mv /usr/local/etc/php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini.disable

COPY ./php-fpm.conf /usr/local/etc/php-fpm.conf
COPY ./www.conf /usr/local/etc/php-fpm.d
RUN rm /usr/local/etc/php-fpm.d/docker.conf /usr/local/etc/php-fpm.d/zz-docker.conf

COPY ./laravel-scheduler /etc/cron.d
COPY ./docker-entrypoint.sh /usr/local/bin

STOPSIGNAL SIGQUIT

WORKDIR /var/www/application-service

ENTRYPOINT ["docker-entrypoint.sh"]