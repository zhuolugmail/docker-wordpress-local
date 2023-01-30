FROM wordpress:6.1.1-apache

RUN docker-php-ext-install pdo_mysql
COPY ./docker-entrypoint.sh /usr/local/bin/
