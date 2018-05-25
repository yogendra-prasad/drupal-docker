FROM debian:stretch-slim

MAINTAINER Yogendra Prasad <yogendra.prasad@srijan.net>

VOLUME ["/var/www/html"]

RUN apt-get update && \
    apt-get install -y \
    apache2 \
    php \
    php-cli \
    libapache2-mod-php \
    php-apcu \
    php-apcu-bc \
    php-gd \
    php-json \
    php-ldap \
    php-mbstring \
    php-mysql \
    php-opcache \
    php-pgsql \
    php-sqlite3 \
    php-xml \
    php-xsl \
    php-zip \
    php-soap \
    php-xdebug \
    php-curl \
    mysql-client


# Enable apache mods.
RUN a2enmod rewrite

RUN mkdir -p /var/www/html/drupal
COPY . /var/www/html/drupal
WORKDIR /var/www/html/drupal

COPY ./web/ports.conf /etc/apache2/

EXPOSE 81
CMD apachectl -D FOREGROUND
