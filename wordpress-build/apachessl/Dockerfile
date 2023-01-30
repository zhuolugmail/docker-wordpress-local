FROM wordpress:latest

RUN docker-php-ext-install pdo_mysql

CMD  a2enmod ssl; \
     a2ensite default-ssl; \
     service apache2 restart; \
     service apache2 stop; \
     apache2-foreground
