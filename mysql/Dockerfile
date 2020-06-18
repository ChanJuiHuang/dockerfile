FROM mysql:latest
ENV MYSQL_ROOT_PASSWORD root
RUN mkdir -p /var/log/mysql && chown mysql:mysql /var/log/mysql
COPY ./mysqld.cnf /etc/mysql/conf.d/mysqld.cnf
