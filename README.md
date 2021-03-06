# dockerfile
## My custom docker file
* [nginx](#nginx)
* [supervisor](#supervisor)
* [redis](#redis)
* [mysql](#mysql)
* [php-fpm](#php-fpm)

### nginx
1. logrotate config of nginx at /etc/logrotate.d/nginx
2. nginx log in /var/log/nginx

### supervisor
1. config file at /etc/supervisor/supervisor.conf

```
program section example:

[program:exmaple-program]
process_name=%(program_name)s_%(process_num)02d
command=<command>
autostart=true
autorestart=true
stopsignal=TERM
numprocs=8
user=root
redirect_stderr=true
stdout_logfile=<log file path>
```

2. included config in /etc/supervisor/conf.d
3. [supervisor website](http://supervisord.org/index.html)

### redis
1. redis.conf at /usr/local/etc/redis/redis.conf
2. users.acl at /usr/local/etc/redis/users.acl

### mysql
1. create predefined password that is "root" for root user
2. you should change your password of thr root user
3. **TZ** that is environment variable can change system time zone
4. slow log and error in /var/log/mysql
5. database data in /var/lib/mysql

### php-fpm
1. php ini file at /usr/local/etc/php
2. php fpm log path is /usr/local/var/log/php-fpm.log
3. /etc/cron.d has laravel scheduler (only for production image tag)
4. xdebug settings in /usr/local/etc/php/conf.d/xdebug.ini (only for development image tag)