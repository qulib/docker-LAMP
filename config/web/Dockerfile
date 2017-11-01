FROM php:5-apache
MAINTAINER Paul Clifford <clifford@queensu.ca>

# custom php.ini file
ADD config/php.ini /usr/local/etc/php/

# additional config
ADD config/php.d/z-memcached.ini /usr/local/etc/php/conf.d

# install modules
RUN apt-get update -y && apt-get install -y libpng-dev memcached php5-memcached
RUN docker-php-ext-install pdo pdo_mysql gd zip opcache
RUN a2enmod rewrite
RUN service apache2 restart
RUN pecl install memcache-3.0.6 && docker-php-ext-enable memcache
