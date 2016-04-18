FROM debian:wheezy

# apt-get dependencies
RUN apt-get update
RUN apt-get install -y git wget curl zip

# apt-get set sources for PHP (wheezy = php5.4)
RUN echo "deb http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list
RUN echo "deb-src http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list
RUN wget https://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg
RUN apt-get update

# apt-get install php
RUN apt-get install -y php5 php5-mysql php5-xdebug php5-json php5-memcache php5-cgi php5-xsl php5-cli php5-fpm php5-imagick php5-readline php5-sqlite php5-common php5-gd php5-curl php5-redis

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
