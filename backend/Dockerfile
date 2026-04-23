# Base image 
FROM php:8.3-cli

# Install sistem dependencies 
RUN apt-get update && apt-get install -y \
    git \                    
    curl \                   
    libpng-dev \            
    libonig-dev \            
    libxml2-dev \            
    zip unzip \              
    libzip-dev \             
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Composer d
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy composer files (untuk cache layer)
COPY composer.json composer.lock ./

# Install PHP dependencies
RUN composer install --no-interaction --no-scripts

# Copy semua kode aplikasi setelah dependencies terinstall
COPY . .

# Set permission agar webserver bisa write ke storage & cache
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 storage \
    && chmod -R 755 bootstrap/cache

# Expose port untuk Laravel development server
EXPOSE 8000

# Jalankan Laravel development server
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]