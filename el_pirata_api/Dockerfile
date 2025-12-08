# FROM php:8.2-fpm

# # Installer les dépendances système
# RUN apt-get update && apt-get install -y \
#     git curl zip unzip \
#     libzip-dev \
#     sqlite3 libsqlite3-dev \
#     && docker-php-ext-configure zip \
#     && docker-php-ext-install pdo pdo_mysql pdo_sqlite zip

# # Installer Composer
# COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# # Définir dossier de travail
# WORKDIR /var/www

# # Copier les fichiers du projet
# COPY . .

# # Installer dépendances PHP
# RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# # Donner les permissions
# RUN chown -R www-data:www-data storage bootstrap/cache

# # Exposer le port utilisé par Laravel
# EXPOSE 8000

# # Lancer Laravel en mode serveur interne
# CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]




FROM php:8.2-cli

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git curl zip unzip sqlite3 libsqlite3-dev libzip-dev \
    && docker-php-ext-configure zip \
    && docker-php-ext-install pdo pdo_mysql pdo_sqlite zip

# Install Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

# Copy project files
COPY . .

# Install dependencies
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Set permissions
RUN chmod -R 777 storage bootstrap/cache

# Railway provides the PORT env var
ENV PORT=8080

EXPOSE 8080

CMD php -S 0.0.0.0:$PORT -t public
