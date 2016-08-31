FROM debian:wheezy

# apt-get dependencies
RUN apt-get update
RUN apt-get install -y git wget curl zip openssh-client

# apt-get set sources for PHP (wheezy = php5.4)
RUN echo "deb http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list
RUN echo "deb-src http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list
RUN wget https://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg

# apt-get set seource for MONO
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb http://download.mono-project.com/repo/debian wheezy main" | tee /etc/apt/sources.list.d/mono-xamarin.list

# Actualize source list
RUN apt-get update

# Install mysql client
RUN apt-get install -y mysql-client

# apt-get install php
RUN apt-get install -y php5 php5-mysql php5-xdebug php5-json php5-cgi php5-xsl php5-cli php5-fpm php5-imagick php5-readline php5-sqlite php5-common php5-gd php5-curl php5-redis php5-zip

RUN apt-get install -y mariadb-client
RUN apt-get install -y apache2 libapache2-mod-php5

# apt-get install python
RUN apt-get install -y python

# disabled xdebug
RUN sed -i "s/^/;/g" /etc/php5/cli/conf.d/20-xdebug.ini

# test PHP version
RUN php -r "if(version_compare(PHP_VERSION, '5.4.0', '<') || version_compare(PHP_VERSION, '5.5.0', '>=')){ echo 'Invalid PHP version '.PHP_VERSION; exit(1); }"

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Mono + nUnit
RUN apt-get install -y mono-complete mono-devel monodevelop-nunit mono-reference-assemblies-*

# test Mono version
RUN (mono -V | grep "version 4.") || (echo "Missing mono version 4" && mono -V && exit 1)