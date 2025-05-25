# Quick Start

Use the `.env` file to set up your local website variables including url and database name / credentials.

    cd cli

Add hosts in custom domain manually in /etc/hosts file.

Optional: If you want to use https, Run the `create-cert` script to create SSL certificates for local https support.

    bash create-cert.sh

Change to main directory and initiate Docker to get up and running!

    cd ..
    docker-compose up

You should now have access to the local site dashboard and SQL database using the settings you provided in the `.env` file. Enjoy!

------

# Detailed Instructions

## Setup (optional: if you wnat https)

In order to use this you will need docker desktop installed and the mkcert utility for creating ssl certificates

check if you have it by using:

    mkcert --version

if you do not, you need to install libnss3-tools.
you'll also need to install mkcert, you can install with homebrew:

    brew install mkcert

## Getting Started (optional: if you want https)

Use the .env file to define your variables. Here you can set up what you want your local site url to be as well as all the database settings that will be applied to your wp-config.php file.

Once you are happy with your setup navigate to the cli folder

    cd cli

### Run scripts (optional: if you want https):

Add hosts in custom domain manually in /etc/hosts file.

    bash create-cert.sh

This uses the mkcert utility to generate ssl certificates and adds them to the certs folder. It may prompt you to enter your password to trust the certs when they are created.

### Run Docker

Now you are ready to go! Change directories back one:

    cd ..

Run docker compose and the images will be downloaded and your local instance will be setup and accessible at your custom url.

    docker-compose -f <docker-compos-...> up


# Additional Notes

Some of the modules were missing in the original setup.  We have to build our
own image to include pdo-mysql.  Otherwise woocommerce may crash due to
mailpoet module error.  Docker build directories are in wordpress-build

Fixed several issues when nginx container is involved.
 - Nginx blocks large files
 - Nginx timeout is too short, cause some demo import fail

Realized we don't have to use nginx for SSL as you can configure apache
for SSL.  Original wordpress image has apache instance running already.

In the process, created several docker compose files for different configuration
variations
 - docker-compose-nginx.yml is from the original setup
    nginx <-> apache and wordpress <-> mysql
 - docker-compose-fpm.yml uses wordpress fpm image that does not have apache
    nginx <-> wordpress with fpm <-> mysql
 - docker-compose-fpm-nossl.yml uses wordpress fpm image that does not have apache and without https
    nginx <-> wordpress with fpm <-> mysql
 - docker-compose-apachessl.yml removes nginx frontend, use apache for ssl
    apache (configured to use ssl) and wordpress <-> mysql

To use these docker-compose yml files, you can create a symbolic link docker-compos.yml to point one of these files.
