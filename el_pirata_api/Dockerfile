FROM php:8.2-fpm

RUN apt-get update && apt-get install -y \
    git curl zip unzip \
    libzip-dev \
    sqlite3 libsqlite3-dev \
    && docker-php-ext-configure zip \
    && docker-php-ext-install pdo pdo_mysql pdo_sqlite zip

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

COPY . .

RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Créer la DB SQLite et donner les permissions
RUN touch /var/www/database/database.sqlite \
    && chown -R www-data:www-data storage bootstrap/cache /var/www/database/database.sqlite

EXPOSE 8000

CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]
