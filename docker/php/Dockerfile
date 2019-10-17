FROM php:7.2-fpm

RUN mv $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini && \
    sed -i -e "s|;session.save_path = "/tmp"|session.save_path = "/tmp" |" /usr/local/etc/php/php.ini && \
    docker-php-ext-install pdo_mysql mbstring && \
    pecl install xdebug-2.6.1 && \
    docker-php-ext-enable xdebug

COPY ./xdebug.ini $PHP_INI_DIR/conf.d/

WORKDIR /data/files/static
