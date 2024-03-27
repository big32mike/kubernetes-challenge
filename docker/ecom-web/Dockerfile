FROM php:7.4-apache

COPY . /var/www/html

ENV DB_HOST='mysql-service'
ENV DB_USER='ecomuser'
ENV DB_PASSWORD='ecompassword'
ENV DB_NAME='ecomdb'

RUN apt-get update \
    && docker-php-ext-install mysqli

EXPOSE 80/tcp
