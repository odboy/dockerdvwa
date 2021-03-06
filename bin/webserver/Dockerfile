FROM php:5.6-apache

COPY sources.list /etc/apt/sources.list

# Install tools && libraries
# removed "apt-get upgrade -y" in order to prevent curl(openssl) error.
RUN apt-get -y update \
    && apt-get -y install --fix-missing apt-utils vim nano wget dialog zip\
    build-essential git curl libcurl3 libcurl3-dev zlib1g-dev \
    libmcrypt-dev libsqlite3-dev libsqlite3-0 mysql-client \
    libicu-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    net-tools iputils-ping netcat
#
# Composer
RUN curl -fsS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN curl https://xdebug.org/files/xdebug-2.5.5.tgz -o /tmp/xdebug-2.5.5.tgz \
    && pecl install /tmp/xdebug-2.5.5.tgz \
    && docker-php-ext-enable xdebug

# PHP5 Extensions
RUN docker-php-ext-install curl \
    && docker-php-ext-install tokenizer \
    && docker-php-ext-install json \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_sqlite \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip \
    && docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-install mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd 

# Enable apache modules and clean apt cache
RUN a2enmod rewrite headers \
    && rm -rf /var/lib/apt/lists/*

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
