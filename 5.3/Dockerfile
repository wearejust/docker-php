FROM andthensome/docker-php-5.3-fpm

MAINTAINER JUST BV

# Install dependencies (needed for composer)
RUN apt-get update -qq \
	&& apt-get install -y -qq \
		libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        locales \
        libicu-dev

# Set timezone
RUN rm /etc/localtime \
	&& ln -s /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime

# Install locales
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
	&& echo "nl_NL.UTF-8 UTF-8" >> /etc/locale.gen \
	&& locale-gen

RUN echo "date.timezone = Europe/Amsterdam" > /usr/local/etc/php/conf.d/timezone.ini \
	&& echo "short_open_tag = off" > /usr/local/etc/php/conf.d/short_open.ini

# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php \
	&& php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer \
	&& php -r "unlink('composer-setup.php');"

EXPOSE 9000

CMD ["php-fpm"]