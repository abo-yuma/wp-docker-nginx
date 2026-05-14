FROM wordpress:php8.2-fpm-alpine

# Install dependencies
RUN apk add --no-cache \
    less \
    mysql-client \
    curl \
    bash

# Install WP-CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp

# Verify installation
RUN wp --info --allow-root