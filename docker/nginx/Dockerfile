FROM nginx:1.13

RUN apt-get update

ADD files /

RUN usermod -u 1000 www-data

WORKDIR /var/www
