FROM php:8.2-fpm

# 1. Installer les dépendances système
# Ajout de libpq-dev (PostgreSQL client library)
# Suppression de sqlite3 et libsqlite3-dev
RUN apt-get update && apt-get install -y \
    git curl zip unzip \
    libzip-dev \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# 2. Installer les extensions PHP
# Activation de pdo_pgsql (PostgreSQL)
# Suppression de pdo_sqlite
RUN docker-php-ext-configure zip \
    && docker-php-ext-install pdo pdo_mysql pdo_pgsql zip

# 3. Installer Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# 4. Définir dossier de travail
WORKDIR /var/www

# 5. Copier les fichiers du projet
COPY . .

# 6. Installer dépendances PHP
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# 7. Donner les permissions
RUN chown -R www-data:www-data storage bootstrap/cache

# 8. Exposer le port utilisé par Laravel
EXPOSE 8000

# 9. Lancer Laravel en mode serveur interne
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]