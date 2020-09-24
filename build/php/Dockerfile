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