FROM php:8.2-cli

WORKDIR /var/www

# Install dependencies
RUN apt-get update && apt-get install -y \
    git curl zip unzip libpq-dev libzip-dev \
    && docker-php-ext-install pdo pdo_pgsql zip

# Install Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Copy application files
COPY . .

# Install dependencies Laravel
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Give permissions
RUN chmod -R 777 storage bootstrap/cache

# =======================================================
# LIGNE CLÉ : EXÉCUTER LES MIGRATIONS DE LA BASE DE DONNÉES
# Ceci résout l'erreur "relation "sessions" does not exist".
# =======================================================
RUN php artisan migrate --force

EXPOSE 8000

# Démarrer l'application
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]