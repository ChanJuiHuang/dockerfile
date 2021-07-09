FROM cjhuang/nginx:latest

RUN apt-get install -y net-tools \
iputils-ping \
tcpdump \
procps \
htop \
less \
vim \
wget

RUN wget -P /root http://nginx.org/download/nginx-1.20.1.tar.gz && \
    tar -xzf /root/nginx-1.20.1.tar.gz -C /root && \
    cp -r /root/nginx-1.20.1/contrib/vim/ /root/.vim && \
    rm -rf /root/nginx-1.20.1.tar.gz /root/nginx-1.18.0

COPY ./vimrc /root/.vimrc
