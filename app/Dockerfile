FROM php:8.3-apache

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y \
    unzip \
    libicu-dev \
    libpng-dev \
    libzip-dev \
    libxml2-dev \
    libonig-dev \
    && docker-php-ext-install \
    mysqli \
    pdo_mysql \
    mbstring \
    intl \
    gd \
    zip \
    xml \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html

COPY ./invoiceplane/ /var/www/html/

RUN mkdir -p /var/www/html/uploads/archive \
    /var/www/html/uploads/customer_files \
    /var/www/html/uploads/temp/mpdf \
    /var/www/html/application/logs \
    && chown -R www-data:www-data /var/www/html \
    && chmod -R 775 /var/www/html/uploads /var/www/html/application/logs