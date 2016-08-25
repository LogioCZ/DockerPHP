FROM ubuntu:xenial

# apt-get dependencies
RUN apt-get update
RUN apt-get install -y git wget curl zip

# apt-get set sources for PHP 5.5
RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 14AA40EC0831756756D7F66C4F4EA0AAE5267A6C

# Actualize source list
RUN apt-get update

# apt-get install php
RUN apt-get install -y php5.5 php5.5-mysql php5.5-xdebug php5.5-json php5.5-cgi php5.5-xsl php5.5-cli php5.5-fpm php5.5-imagick php5.5-readline php5.5-sqlite php5.5-common php5.5-gd php5.5-curl php5.5-redis

# apt-get install python
RUN apt-get install -y python

# disabled xdebug
RUN sed -i "s/^/;/g" /etc/php/5.5/cli/conf.d/20-xdebug.ini

# test PHP version
RUN php -r "if(version_compare(PHP_VERSION, '5.5.0', '<') || version_compare(PHP_VERSION, '5.6.0', '>=')){ echo 'Invalid PHP version '.PHP_VERSION; exit(1); }"

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Mono + nUnit
RUN apt-get install -y mono-complete mono-devel monodevelop-nunit mono-reference-assemblies-*

# test Mono version
RUN (mono -V | grep "version 4.") || (echo "Missing mono version 4" && mono -V && exit 1)