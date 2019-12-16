FROM php:7.2-apache
LABEL maintainer="Andrew DaCosta <adacosta@queensu.ca>"

# # custom php.ini file
ADD config/php.ini /usr/local/etc/php/

# # additional config
ADD config/php.d/z-memcached.ini /usr/local/etc/php/conf.d/memcached.ini

# # Set the Drush version.
ENV DRUSH_VERSION 8.1.18

# # Install Drush 8 with the phar file.
RUN curl -fsSL -o /usr/local/bin/drush "https://github.com/drush-ops/drush/releases/download/$DRUSH_VERSION/drush.phar" && chmod +x /usr/local/bin/drush

# # change ownership of drupal webroot
RUN chown -R www-data:www-data /var/www/html/

# # install modules
RUN apt-get update -y && apt-get install -y libpng-dev
RUN docker-php-ext-install pdo pdo_mysql gd zip opcache 

# # fix for multi-byte error in Drupal 7.x 
RUN docker-php-ext-install mbstring

# memcache 3.0.8
RUN apt-get update -y && apt-get install -y libmemcached-dev 
RUN pecl install memcached-3.1.3
#RUN echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini
RUN docker-php-ext-enable memcached

#jsmin
RUN pecl install jsmin
RUN docker-php-ext-enable jsmin

# mysql client
#RUN apt-get update && apt-get install -y mysql-client && rm -rf /var/lib/apt
#RUN apt-get update && apt-get install -y mariadb-client && rm -rf /var/lib/apt
RUN apt-get update && apt-get install -y default-mysql-client && rm -rf /var/lib/apt
RUN a2enmod rewrite
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
RUN service apache2 restart

# change ownership of drupal webroot
RUN chown -R www-data:www-data /var/www/html/
