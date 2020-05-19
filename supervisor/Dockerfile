FROM ubuntu:20.04

RUN apt-get update && apt-get install -y supervisor

ENTRYPOINT ["supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]
