FROM php:5.6-fpm

MAINTAINER JUST BV

# Install dependencies (needed for composer)
RUN apt-get clean && apt-get update -qq
RUN apt-get install -y -qq unzip git zlib1g-dev locales libpng-dev zlib1g-dev libicu-dev g++
RUN rm -rf /var/lib/apt/lists/*

# Install locales
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "nl_NL.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql gd
RUN docker-php-ext-configure intl && docker-php-ext-install intl

RUN echo "date.timezone = Europe/Amsterdam" > /usr/local/etc/php/conf.d/timezone.ini
RUN echo "short_open_tag = off" > /usr/local/etc/php/conf.d/short_open.ini

# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer
RUN php -r "unlink('composer-setup.php');"

# Install global performance booster
RUN composer global require "hirak/prestissimo:^0.3"

EXPOSE 9000

CMD ["php-fpm"]