FROM ubuntu:xenial

# apt-get dependencies
RUN apt-get update
RUN apt-get install -y git wget curl zip

# apt-get set sources for PHP 5.6
RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 14AA40EC0831756756D7F66C4F4EA0AAE5267A6C

# Actualize source list
RUN apt-get update

# apt-get install php
RUN apt-get install -y php5.6 php5.6-mysql php5.6-xdebug php5.6-json php5.6-cgi php5.6-xsl php5.6-cli php5.6-fpm php5.6-imagick php5.6-readline php5.6-sqlite php5.6-common php5.6-gd php5.6-curl php5.6-redis php5.6-zip

RUN apt-get install -y mariadb-client
RUN apt-get install -y apache2 libapache2-mod-php5.6

# apt-get install python
RUN apt-get install -y python

# disabled xdebug
RUN sed -i "s/^/;/g" /etc/php/5.6/cli/conf.d/20-xdebug.ini

# test PHP version
RUN php -r "if(version_compare(PHP_VERSION, '5.6.0', '<') || version_compare(PHP_VERSION, '5.7.0', '>=')){ echo 'Invalid PHP version '.PHP_VERSION; exit(1); }"

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Mono + nUnit
RUN apt-get install -y mono-complete mono-devel monodevelop-nunit mono-reference-assemblies-*

# test Mono version
RUN (mono -V | grep "version 4.") || (echo "Missing mono version 4" && mono -V && exit 1)