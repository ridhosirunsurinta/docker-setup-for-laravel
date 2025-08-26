FROM php:8.2-fpm-alpine

# System deps
RUN apk add --no-cache \
    git curl zip unzip icu-dev oniguruma-dev \
    libpng libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
    libzip-dev libxml2-dev bash

# PHP extensions
RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    --with-webp \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql mbstring zip intl bcmath exif pcntl

# Opcache (opsional)
RUN docker-php-ext-install opcache

# Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Workdir
WORKDIR /var/www

# Permissions ringan untuk dev
RUN addgroup -g 1000 app && adduser -G app -g app -s /bin/sh -D app \
    && chown -R app:app /var/www
USER app
