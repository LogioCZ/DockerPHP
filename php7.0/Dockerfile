FROM ubuntu:xenial

# apt-get dependencies
RUN apt-get update
RUN apt-get install -y git wget curl zip

# apt-get set sources for PHP 7.0
RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 14AA40EC0831756756D7F66C4F4EA0AAE5267A6C

# Actualize source list
RUN apt-get update

# apt-get install php
RUN apt-get install -y php7.0 php7.0-mysql php7.0-xdebug php7.0-json php7.0-cgi php7.0-xsl php7.0-cli php7.0-fpm php7.0-imagick php7.0-readline php7.0-sqlite php7.0-common php7.0-gd php7.0-curl php7.0-redis

# apt-get install python
RUN apt-get install -y python

# disabled xdebug
RUN sed -i "s/^/;/g" /etc/php/7.0/cli/conf.d/20-xdebug.ini

# test PHP version
RUN php -r "if(version_compare(PHP_VERSION, '7.0.0', '<') || version_compare(PHP_VERSION, '7.1.0', '>=')){ echo 'Invalid PHP version '.PHP_VERSION; exit(1); }"

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Mono + nUnit
RUN apt-get install -y mono-complete mono-devel monodevelop-nunit mono-xbuild mono-runtime mono-reference-assemblies-*

# test Mono version
RUN (mono -V | grep "version 4.") || (echo "Missing mono version 4" && mono -V && exit 1)