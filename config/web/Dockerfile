FROM php:5.5.30-apache
LABEL maintainer="Paul Clifford <clifford@queensu.ca>"

# custom php.ini file
ADD config/php.ini /usr/local/etc/php/

# additional config
ADD config/php.d/z-memcached.ini /usr/local/etc/php/conf.d

# install modules
RUN apt-get update -y && apt-get install -y libpng-dev memcached
RUN docker-php-ext-install pdo pdo_mysql gd zip opcache 
RUN docker-php-ext-install mbstring
RUN pecl install memcache-3.0.8 && echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini && docker-php-ext-enable memcache
RUN a2enmod rewrite
RUN service apache2 restart
