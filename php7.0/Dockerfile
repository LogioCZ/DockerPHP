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
RUN apt-get install -y php7.0 php7.0-mysql php7.0-xdebug php7.0-json php7.0-cgi php7.0-xsl php7.0-cli php7.0-fpm php7.0-imagick php7.0-readline php7.0-sqlite php7.0-common php7.0-gd php7.0-curl php7.0-redis

# disabled xdebug
RUN sed -i "s/^/;/g" /etc/php/7.0/cli/conf.d/20-xdebug.ini

# test PHP version
RUN php -r "if(version_compare(PHP_VERSION, '7.0.0', '<') || version_compare(PHP_VERSION, '7.1.0', '>=')){ echo 'Invalid PHP version '.PHP_VERSION; exit(1); }"

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
