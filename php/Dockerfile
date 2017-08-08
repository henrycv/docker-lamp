##
## Name: docker-lamp-php
## Dockerfile to build a PHP-Apache stack image
##
FROM php:5.6.31-apache

MAINTAINER Henry Carbajal <entidad.estelar@gmail.com>

# Setted fix to issue "debconf: unable to initialize frontend: Dialog"
# http://askubuntu.com/questions/506158/unable-to-initialize-frontend-dialog-when-using-ssh
ENV DEBIAN_FRONTEND noninteractive

# Mount the html/ folder
VOLUME /var/www/html

# Update sources
RUN apt-get -y update

# Packages installations
RUN apt-get -y install \
    # Install CURL tool
    curl \
    # Install Wget package for testing tasks
    wget \
    # Install Vim editor
    vim \
    # Install PHP XSL
    php5-xsl \
    # Install PHP XMLRPC
    php5-xmlrpc \
    # Install PHP SNMP
    php5-snmp \
    # Install PSPELL
    php5-pspell \
    # Install PHP MEMCACHE
    php5-memcache \
    # Install PHP GD
    php5-gd  \
    # Install PHP APC
    php-apc \
    # Install PHP Mcrypt
    php5-mcrypt \
    # Install MySQLI extension
    php5-mysqli \
    # Install MySQL extension
    php5-mysqlnd \
    # Install PHP XDebug
    php5-xdebug \
    # # Install NodeJS
    nodejs \
    # Install NPM
    npm

# # Enable Apache mod rewrite
RUN a2enmod rewrite

# # Enabling module expires.
RUN a2enmod file_cache
RUN a2enmod expires
RUN a2enmod headers
RUN a2enmod ssl

# # Enable PHP Mcrypt extension
# RUN php5enmod mcrypt

# Copy the customized Apache config on guest machine:
#    "/etc/apache2/apache2.conf"
# COPY ./config/apache2.conf /etc/apache2/apache2.conf

# Copy the customized PHP development config on guest machine:
# COPY ./config/php.ini /etc/php5/apache2/php.ini

# SSL 
COPY ./config/86701868-_.vidrieravirtual.com.cert /etc/ssl/certs/
COPY ./config/86701868-_.vidrieravirtual.com.key /etc/ssl/private/

# Copy the "test.dev" vhost file on guest machine
COPY ./config/sites-available/* /etc/apache2/sites-available/

# Remove all sites enabled by default
RUN rm -rf /etc/apache2/sites-enabled/*

# Enable all vhost files
RUN ln -s /etc/apache2/sites-available/vidrieravirtual* /etc/apache2/sites-enabled/

# Install PHP Composer globally
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Install PHP Symfony framework tool globally
RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony
RUN chmod a+x /usr/local/bin/symfony
