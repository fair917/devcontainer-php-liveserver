FROM --platform=amd64 mcr.microsoft.com/devcontainers/php:8.3-apache-bookworm

ENV TZ Asia/Tokyo
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

RUN a2enmod ssl && \
    a2ensite default-ssl

COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY ./assets/serve /usr/local/bin/
COPY ./assets/apache2/ports.conf ./assets/apache2/apache2.conf /etc/apache2/
COPY ./assets/apache2/000-default.conf ./assets/apache2/default-ssl.conf /etc/apache2/sites-available/