FROM php:8.2-cli

WORKDIR /var/www

# Install system dependencies, including PostgreSQL library headers
RUN apt-get update && apt-get install -y \
    git curl zip unzip libpq-dev libzip-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Install PHP extensions, including pdo_pgsql
RUN docker-php-ext-install pdo pdo_pgsql zip

# Copy application files
COPY . .

# Install dependencies Laravel
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Give permissions
RUN chmod -R 777 storage bootstrap/cache

# =======================================================
# LIGNE CLÉ : EXÉCUTER LES MIGRATIONS DE LA BASE DE DONNÉES
# Ceci est exécuté APRÈS l'installation du driver.
# =======================================================
RUN php artisan migrate --force

EXPOSE 8000

# Démarrer l'application
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]