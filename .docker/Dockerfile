FROM php:7.2-apache
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y git zip unzip libjpeg62-turbo-dev libfreetype6-dev libzip-dev libpq-dev libicu-dev libpng-dev libjpeg-dev libwebp-dev libxml2-dev libxslt-dev \
    && docker-php-ext-install pdo pdo_pgsql pdo_mysql mysqli bcmath intl soap xsl zip sockets \
    && a2enmod rewrite
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd
#install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#xdebug
RUN pecl install xdebug-2.7.2 && docker-php-ext-enable xdebug
ARG XDEBUG_INI=/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.default_enable = off" >> ${XDEBUG_INI} \
    && echo "xdebug.remote_enable = on" >> ${XDEBUG_INI} \
    && echo "xdebug.remote_autostart = off" >> ${XDEBUG_INI} \
    && echo "xdebug.remote_connect_back = off" >> ${XDEBUG_INI} \
    && echo "xdebug.remote_port = 9001" >> ${XDEBUG_INI} \
    && echo "xdebug.remote_host = host.docker.internal" >> ${XDEBUG_INI}
WORKDIR /app
EXPOSE 80
