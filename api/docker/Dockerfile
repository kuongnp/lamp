FROM php:apache-bullseye

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apt-get update && apt-get install -y git libzip-dev unzip \
    && docker-php-ext-install zip \
    && a2enmod rewrite headers \
    && a2enconf docker-php

#enable systemd
RUN apt-get update && apt-get install -y init && apt-get clean all
# copy virtual host config
COPY ./api.conf /etc/apache2/sites-available
# enable virtual host
RUN a2ensite api.conf
RUN a2dissite 000-default.conf

WORKDIR /var/www/api
CMD ["/sbin/init"]
