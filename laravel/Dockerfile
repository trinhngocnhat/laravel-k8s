# Sử dụng PHP 8.1 làm base image
FROM php:8.2-fpm

# Cài đặt các dependencies cần thiết
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    && docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd

# Cài đặt Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Thiết lập thư mục làm việc
WORKDIR /var/www

# Sao chép toàn bộ project Laravel vào container
COPY . .

# Cấp quyền cho thư mục storage và bootstrap/cache
RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache
RUN chmod -R 775 /var/www/storage /var/www/bootstrap/cache

# Cài đặt các package Laravel
RUN composer install --no-dev --optimize-autoloader

# Expose port
EXPOSE 9000

CMD ["php-fpm"]
