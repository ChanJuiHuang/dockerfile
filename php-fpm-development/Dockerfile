FROM cjhuang/php-fpm

RUN apt-get update && apt-get install -y vim \
    htop

RUN pecl install xdebug

COPY ./vimrc /root/.vimrc

COPY ./php-ini/php.ini-development /usr/local/etc/php/php.ini
RUN mv /usr/local/etc/php/conf.d/xdebug.ini.disable /usr/local/etc/php/conf.d/xdebug.ini
