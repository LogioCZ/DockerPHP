FROM ubuntu:xenial

# apt-get set sources for PHP 7.1
RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list \
 && echo "deb-src http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" >> /etc/apt/sources.list \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 14AA40EC0831756756D7F66C4F4EA0AAE5267A6C \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
 && echo "deb http://download.mono-project.com/repo/debian wheezy main" | tee /etc/apt/sources.list.d/mono-xamarin.list

# apt-get dependencies
RUN apt-get update \
 && apt-get install -y \
      apache2 \
      curl \
      git \
      make \
      mariadb-client \
      mono-complete \
      mono-devel \
      mono-reference-assemblies-* \
      mono-runtime \
      mono-xbuild \
      monodevelop-nunit \
      nuget \
      openssh-client \
      python \
      wget \
      zip

RUN a2enmod rewrite

COPY etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf

# test Mono version
RUN (mono -V | grep "version 4.") || (echo "Missing mono version 4" && mono -V && exit 1)

# apt-get install php
RUN apt-get install -y \
      libapache2-mod-php7.1 \
      php7.1 \
      php7.1-cgi \
      php7.1-cli \
      php7.1-common \
      php7.1-curl \
      php7.1-fpm \
      php7.1-gd \
      # php7.1-imagick \
      php7.1-json \
      php7.1-mysql \
      php7.1-readline \
      # php7.1-redis \
      php7.1-sqlite \
      # php7.1-xdebug \
      php7.1-xsl \
      php7.1-zip

# disabled xdebug
# RUN sed -i "s/^/;/g" /etc/php/7.1/cli/conf.d/20-xdebug.ini

# test PHP version
RUN php -r "if(strpos(PHP_VERSION, '7.1.') !== 0){ echo 'Invalid PHP version '.PHP_VERSION; exit(1); }"

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
