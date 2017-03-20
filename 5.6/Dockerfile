FROM php:5.6-fpm

MAINTAINER JUST BV

# Set timezone
RUN rm /etc/localtime \
	&& ln -s /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql

RUN echo "date.timezone = Europe/Amsterdam" > /usr/local/etc/php/conf.d/timezone.ini \
	&& echo "short_open_tag = off" > /usr/local/etc/php/conf.d/short_open.ini

EXPOSE 9000

CMD ["php-fpm"]