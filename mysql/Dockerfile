FROM mysql:5.7

ENV http_proxy http://proxy.hogehoge:8080
ENV hppts_proxy https://proxy.hogehoge:8080

COPY ./my.cnf /etc/mysql/conf.d/

RUN /etc/init.d/mysql start

