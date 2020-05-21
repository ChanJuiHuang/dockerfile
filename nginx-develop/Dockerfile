FROM nginx:stable

RUN rm -rf /etc/cron.daily/*
RUN apt-get update && apt-get install -y logrotate

RUN apt-get install -y net-tools \
iputils-ping \
tcpdump \
vim

RUN groupadd -g 999 -r docker && useradd -u 999 -g 999 -r docker

COPY ./logrotate.d/nginx /etc/logrotate.d/
COPY ./docker-entrypoint.sh /usr/local/bin/
COPY ./vimrc /root/.vimrc 

STOPSIGNAL SIGQUIT

ENTRYPOINT ["docker-entrypoint.sh"]
