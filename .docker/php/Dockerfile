FROM php:8.1-apache

RUN apt-get update && \
    apt-get -y install zip

# Configure and install PHP extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

# Change memory_limit
RUN cd /usr/local/etc/php/conf.d/ && \
    echo 'memory_limit = -1' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini

# Install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install symfony cli
RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash
RUN apt -y install symfony-cli


