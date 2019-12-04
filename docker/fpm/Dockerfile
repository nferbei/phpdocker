FROM php:7.3-fpm
ARG COMPOSER_VERSION

RUN apt-get update

RUN apt-get install -y gnupg gnupg2 gnupg1 wget git zip unzip ssh
RUN docker-php-ext-install pdo_mysql mbstring bcmath

RUN docker-php-ext-enable opcache \
    && echo "opcache.enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.enable_cli=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN wget https://getcomposer.org/installer -O - -q \
    | php -- --install-dir=/bin --filename=composer  --version=$COMPOSER_VERSION --quiet

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs

