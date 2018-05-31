FROM debian:stretch-slim

MAINTAINER Yogendra Prasad <yogendra.prasad@srijan.net>

VOLUME ["/var/www/html"]


RUN apt-get update --fix-missing \
    && apt-get install -y \
    gnupg \
    curl wget git htop supervisor vim openssh-server software-properties-common netcat

COPY ./docker-utils/apache2/source-list/linode.list /etc/apt/sources.list.d/

RUN apt-key update && apt-get update --fix-missing

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
    php-fpm \
    mysql-client \
    libapache2-mod-fastcgi


RUN a2enmod rewrite headers fastcgi actions
COPY ./docker-utils/apache2/mods-enabled/*.conf /etc/apache2/mods-enabled
COPY ./docker-utils/apache2/sites/*.conf /etc/apache2/sites-available
COPY ./docker-utils/supervisord/*.conf /etc/supervisor/conf.d/
COPY ./docker-utils/scripts /scripts/
COPY ./docker-utils/apache2/keys/* /etc/apache2/ssl/
RUN chmod u+x /scripts/*.sh

RUN mkdir -p /var/www/html/drupal
COPY . /var/www/html/drupal
WORKDIR /var/www/html/drupal

RUN service php7.0-fpm start
COPY ./docker-utils/apache2/ports.conf /etc/apache2/

EXPOSE 443

CMD ["/scripts/start-services.sh"]
