FROM php:7.2-fpm-buster

RUN apt-get update \
    && apt-get -y --no-install-recommends install \
    libmemcached-dev zlib1g-dev \
    libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev \
	libmcrypt-dev \
	libmagickwand-dev \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev \
	curl libcurl4-gnutls-dev \
	libmagickwand-dev \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN pecl install mcrypt && docker-php-ext-enable mcrypt
RUN docker-php-ext-install gettext && docker-php-ext-enable gettext
RUN pecl install memcached && docker-php-ext-enable memcached
RUN docker-php-ext-install gd mysqli bcmath intl xml curl hash zip dom session opcache
RUN docker-php-ext-enable mysqli bcmath intl xml curl hash zip dom session opcache gd

# DO NOT install php7.3-xdebug package for site running in production! It will slow it down significantly.

COPY ./php.ini /etc/php/7.2/fpm/conf.d/90-php.ini
COPY ./php.ini /etc/php/7.2/cli/conf.d/90-php.ini

RUN usermod -u 1000 www-data

WORKDIR "/var/www/bitrix"

EXPOSE 9000
