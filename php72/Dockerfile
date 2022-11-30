FROM php:7.2-fpm-buster

RUN apt-get update \
    && apt-get -y --no-install-recommends install \
    libmemcached-dev zlib1g-dev \
    libssl-dev \
    libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev \
	libjpeg-dev \
	libmcrypt-dev \
	libmagickwand-dev \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev \
	curl libcurl4-gnutls-dev \
	libmagickwand-dev \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN pecl install mcrypt && docker-php-ext-enable mcrypt
RUN docker-php-ext-install mbstring gettext && docker-php-ext-enable mbstring gettext
RUN pecl install memcached && docker-php-ext-enable memcached
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd mysqli bcmath intl xml curl hash zip dom session opcache
RUN docker-php-ext-enable mysqli bcmath intl xml curl hash zip dom session opcache gd

# DO NOT install php7.3-xdebug package for site running in production! It will slow it down significantly.

COPY ./php.ini /usr/local/etc/php/php.ini
COPY ./php.ini /etc/php/7.2/cli/conf.d/90-php.ini

RUN usermod -u 1001 www-data

WORKDIR "/var/www/bitrix"

EXPOSE 9000
