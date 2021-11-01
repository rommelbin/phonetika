FROM php:7.4-fpm
ENV CASH_PATH /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND noninteractive
WORKDIR "/var/www/"

RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libpq-dev\
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    nano \
    unzip \
    git \
    curl && \
    rm -rf ${CASH_PATH}

EXPOSE 9000
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql
RUN docker-php-ext-install pdo pdo_pgsql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

CMD chown -R www-data:www-data /var/www && chmod -R 775 /var/www && composer install && php artisan migrate && php-fpm
