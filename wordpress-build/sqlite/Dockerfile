FROM wordpress:6.1.1-apache

RUN  apt update
RUN  apt install -y git
RUN  git clone https://github.com/aaemnnosttv/wp-sqlite-db.git /var/wp-sqlite-db

RUN  docker-php-ext-install pdo_mysql

COPY ./docker-entrypoint.sh /usr/local/bin/
