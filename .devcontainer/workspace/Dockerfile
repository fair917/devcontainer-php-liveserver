FROM --platform=amd64 mcr.microsoft.com/devcontainers/php:8.1-apache-bookworm

ENV TZ Asia/Tokyo
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

RUN apt-get update && \
    apt-get install -y \
        libicu-dev \
        libzip-dev \
        imagemagick \
        libmagickwand-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN a2enmod ssl && \
    a2ensite default-ssl && \
    docker-php-ext-install exif intl zip mysqli && \
    pecl install igbinary && \
    curl -OL https://pecl.php.net/get/imagick-3.7.0.tgz && \
    tar zxf imagick-3.7.0.tgz && \
    cd imagick-3.7.0/ && \
    phpize && \
    ./configure && \
    make && make install && \
    docker-php-ext-enable igbinary imagick && \
    rm -rf /root/imagick-3.7.0

COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY ./assets/serve /usr/local/bin/
COPY ./assets/apache2/ports.conf ./assets/apache2/apache2.conf /etc/apache2/
COPY ./assets/apache2/000-default.conf ./assets/apache2/default-ssl.conf /etc/apache2/sites-available/