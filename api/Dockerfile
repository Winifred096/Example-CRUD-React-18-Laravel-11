# Stage 1: Composer with PHP 8.2
FROM php:8.2-cli AS composer

RUN apt-get update && apt-get install -y unzip git curl zip libzip-dev \
    && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /app

COPY composer.json composer.lock* ./
RUN composer install --no-scripts --no-autoloader

# Stage 2: Laravel app
FROM php:8.2-fpm

WORKDIR /var/www/html

RUN apt-get update && apt-get install -y libzip-dev unzip \
    && docker-php-ext-install zip pdo pdo_mysql

COPY . .

COPY --from=composer /app/vendor ./vendor

RUN chown -R www-data:www-data /var/www/html

EXPOSE 9000

CMD ["php-fpm"]
