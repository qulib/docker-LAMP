FROM php:5-apache
MAINTAINER Paul Clifford <clifford@queensu.ca>

# custom php.ini file
ADD config/php.ini /usr/local/etc/php/

# additional config
ADD config/php.d/z-memcached.ini /usr/local/etc/php/conf.d

# install modules
RUN apt-get update -y && apt-get install -y libpng-dev memcached
RUN docker-php-ext-install pdo pdo_mysql gd zip opcache
RUN a2enmod rewrite
RUN service apache2 restart
RUN yes|CFLAGS="-fgnu89-inline" pecl install memcache-3.0.8
RUN docker-php-ext-enable memcache
