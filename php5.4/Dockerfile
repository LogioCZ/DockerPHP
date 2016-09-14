FROM debian:wheezy

RUN apt-get update && apt-get install -y wget ca-certificates

# apt-get set sources for PHP (wheezy = php5.4)
# apt-get set seource for MONO
RUN echo "deb http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list \
 && echo "deb-src http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list \
 && wget https://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg \
 && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
 && echo "deb http://download.mono-project.com/repo/debian wheezy main" | tee /etc/apt/sources.list.d/mono-xamarin.list

# apt-get dependencies
RUN apt-get update \
 && apt-get install -y \
      apache2 \
      curl \
      git \
      make \
      mono-complete \
      mono-devel \
      mono-reference-assemblies-* \
      mono-runtime \
      mono-xbuild \
      monodevelop-nunit \
      mysql-client \
      nuget \
      nunit \
      openssh-client \
      python \
      zip

RUN a2enmod rewrite

COPY etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf

# test Mono version
RUN (mono -V | grep "version 4.") || (echo "Missing mono version 4" && mono -V && exit 1)

# apt-get install php
RUN apt-get install -y \
      libapache2-mod-php5 \
      php5 \
      php5-cgi \
      php5-cli \
      php5-common \
      php5-curl \
      php5-fpm \
      php5-gd \
      php5-imagick \
      php5-json \
      php5-mysql \
      php5-readline \
      php5-redis \
      php5-sqlite \
      php5-xdebug \
      php5-xsl

# disabled xdebug
RUN sed -i "s/^/;/g" /etc/php5/cli/conf.d/20-xdebug.ini

# test PHP version
RUN php -r "if(version_compare(PHP_VERSION, '5.4.0', '<') || version_compare(PHP_VERSION, '5.5.0', '>=')){ echo 'Invalid PHP version '.PHP_VERSION; exit(1); }"

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
