FROM debian:jessie

MAINTAINER Yogendra Prasad <yogendra.prasad@srijan.net>

VOLUME ["/var/www/html"]

RUN apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y \
    apache2 \
    php5 \
    php5-mysql \
    php5-mcrypt \
    php5-cli \
    php5-gd \
    php5-curl\
    mysql-client



# Enable apache mods.
RUN a2enmod php5
RUN a2enmod rewrite

RUN mkdir -p /var/www/html/drupal
COPY . /var/www/html/drupal
WORKDIR /var/www/html/drupal


COPY ./web/ports.conf /etc/apache2/

EXPOSE 81
CMD apachectl -D FOREGROUND
