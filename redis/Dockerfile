FROM redis:latest

COPY ./redis.conf /usr/local/etc/redis/redis.conf
RUN touch /usr/local/etc/redis/users.acl

CMD ["redis-server", "/usr/local/etc/redis/redis.conf"]
