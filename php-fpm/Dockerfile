FROM php:7.2-fpm

ENV ACCEPT_EULA=Y

# Install basic packages and extensions
RUN apt-get update \
  && apt-get install -y apt-transport-https build-essential debconf-utils zlib1g-dev locales libzip-dev curl libbz2-1.0 libicu-dev wget gnupg \
  && docker-php-ext-install zip opcache

RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

# Install SQL Server extensions
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get install -y msodbcsql17 mssql-tools
RUN apt-get install -y unixodbc-dev libgssapi-krb5-2
RUN pecl install sqlsrv pdo_sqlsrv xdebug
RUN docker-php-ext-enable sqlsrv pdo_sqlsrv xdebug

# composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH=$PATH:/home/www-data/.composer/vendor/bin

# Limpar Cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

