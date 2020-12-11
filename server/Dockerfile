FROM php:7.4-fpm
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

WORKDIR /var/www
# Install dependencies
RUN apt-get update && apt-get install -y \
  build-essential \
  libmcrypt-dev \
  mariadb-client \
  libpng-dev \
  libjpeg62-turbo-dev \
  libfreetype6-dev \
  locales \
  zip \
  jpegoptim optipng pngquant gifsicle \
  vim \
  unzip \
  git \
  curl iputils-ping npm
# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*


RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable pdo_mysql
RUN apt-get update && apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql

#RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
RUN docker-php-ext-install gd


# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
