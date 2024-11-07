# Use PHP 8.2 with Apache
FROM php:8.2-apache

# Install necessary system dependencies and PHP extensions
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libicu-dev \
    libpq-dev \
    && docker-php-ext-install intl pdo pdo_mysql

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Set the working directory
WORKDIR /var/www/html

# Copy the Symfony project files to the working directory
COPY . .

# Set the document root to Symfony's public directory
RUN sed -i 's|DocumentRoot /var/www/html|DocumentRoot /var/www/html/public|' /etc/apache2/sites-available/000-default.conf

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install project dependencies based on composer.json
RUN composer install --no-dev --optimize-autoloader

# Expose the port that Apache will run on
EXPOSE 80

# Start the Apache server
CMD ["apache2-foreground"]
