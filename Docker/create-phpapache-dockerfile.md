Dockerfile content
```bash
# Based on official php apache image
FROM php:7.2.6-apache
LABEL maintainer "simeon.bobylev@gmail.com"

# Set Europe/Zurich timezone
RUN ln -fs /usr/share/zoneinfo/Europe/Zurich /etc/localtime

# Install some usefull packages
RUN apt-get update && apt-get install -y -q vim git wget zip

# Copy php.ini with custom configuration
COPY php.ini /usr/local/etc/php/php.ini

# Install pdo_mysql for php
RUN docker-php-ext-install pdo_mysql

# Install composer
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/1b137f8bf6db3e79a38a5bc45324414a6b1f9df2/web/installer -O - -q | php -- --quiet
RUN mv composer.phar /usr/local/bin/composer

# Secure apache
RUN sed -i 's/ServerSignature On/ServerSignature Off/g' /etc/apache2/conf-available/security.conf
RUN sed -i 's/ServerTokens OS/ServerTokens Prod/g' /etc/apache2/conf-available/security.conf

# Copy apache custom configuration
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

# Enable apache rewrite module
RUN a2enmod rewrite
```
