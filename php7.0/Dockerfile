FROM debian:jessie

# apt-get dependencies
RUN apt-get update
RUN apt-get install -y git wget curl zip

# apt-get set sources for PHP (jessie = php7.0)
RUN echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list
RUN echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list
RUN wget https://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg
RUN apt-get update

# apt-get install php
RUN apt-get install -y php php-mysql php-xdebug php-json php-memcache php-cgi php-xsl php-cli php-fpm php-imagick php-readline php-sqlite php-common php-gd php-curl php-redis

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
