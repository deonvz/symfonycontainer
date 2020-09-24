# # In this docker file, we’ll install PHP packages on Ubuntu image with composer and will copy the www.conf and php-fpm.conf files from the host and add the content of the guest folders.
# FROM ubuntu:18.04
# # Ubuntu Focal 20.04 stops on a timezone prompt
# RUN apt-get -y update
# # RUN apt-get install -my \
# # Non interactive line below is because docker build stops awaiting a timezone
# RUN DEBIAN_FRONTEND="noninteractive" \ 
# TZ=Africa/Johannesburg \
# apt-get -y install tzdata
# RUN apt-get -qq -y install -my \
#   curl \
#   wget \
#   php-curl \
#   php-fpm \
#   php-gd \
#   php-xsl \
#   # Mysql below
#   #php-mysqlnd \
#   #MariaDB below
#   #pdo_mysql \
#   #php-mcrypt \
#   php-cli \
#   php-intl \
#   php-bz2 \
#   php-zip \
#   php-mbstring \
#   git \
#   zip \
#   php-apcu \
#   php-redis \
#   php-opcache
# #RUN pecl install apcu  
# #RUN docker-php-ext-enable apcu  
# RUN mkdir /run/php
# # Copy over the configs
# ADD conf/www.conf /etc/php/7.2/fpm/pool.d/www.conf
# ADD conf/php-fpm.conf /etc/php/7.2/fpm/php-fpm.conf

# RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
# RUN php composer-setup.php
# RUN php -r "unlink('composer-setup.php');"
# RUN mv composer.phar /usr/local/bin/composer
# RUN chmod +x /usr/local/bin/composer

# # WORKDIR /usr/src/app
# # COPY --chown=1000:1000 apps/my-symfony-app /usr/src/app
# WORKDIR /var/www

# EXPOSE 9000
# #RUN PATH=$PATH:/usr/src/apps/vendor/bin:bin
# #CMD ["php-fpm7.2"]

# # The lines below is only because mariadb`s pdo_mysql. The extension is not found above as it is looking in Ubuntu and not php
# #FROM php:7.2-apache
# FROM php:7.2-fpm
# RUN docker-php-ext-install pdo pdo_mysql
# #COPY my-php-files/ /var/www/html/

# CMD ["php"]

FROM php:7.2-fpm

RUN docker-php-ext-install pdo_mysql

RUN pecl install apcu

RUN apt-get update && \
apt-get install -y \
libzip-dev

RUN docker-php-ext-install zip
RUN docker-php-ext-enable apcu

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer    

WORKDIR /var/www

COPY --chown=${LOCAL_USER} apps/my-symfony-app /var/www

# Copy over the configs
ADD build/php/conf/www.conf /etc/php/7.2/fpm/pool.d/www.conf
ADD build/php/conf/php-fpm.conf /etc/php/7.2/fpm/php-fpm.conf

RUN PATH=$PATH:/var/www/vendor/bin:bin