FROM ubuntu:xenial

# apt-get dependencies
RUN apt-get update
RUN apt-get install -y git wget curl zip

# apt-get set sources for PHP 7.1
RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 14AA40EC0831756756D7F66C4F4EA0AAE5267A6C
RUN apt-get update

# apt-get install php
RUN apt-get install -y php7.1 php7.1-mysql php7.1-json php7.1-cgi php7.1-xsl php7.1-cli php7.1-fpm php7.1-readline php7.1-sqlite php7.1-common php7.1-gd php7.1-curl

# @todo add missing packages
# RUN apt-get install -y php7.1-redis php7.1-xdebug php7.1-imagick

# disabled xdebug
#RUN sed -i "s/^/;/g" /etc/php/7.1/cli/conf.d/20-xdebug.ini

# test PHP version
RUN php -r "if(strpos(PHP_VERSION, '7.1.') !== 0){ echo 'Invalid PHP version '.PHP_VERSION; exit(1); }"

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
