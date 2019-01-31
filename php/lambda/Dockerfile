FROM amazonlinux:2017.03.1.20170812

RUN yum update -y && \
    yum install -y autoconf \
    bison \
    gcc \
    gcc-c++ \
    make \
    libcurl-devel \
    libxml2-devel \
    tar \
    gzip \
    zip \
    git

WORKDIR /tmp
RUN curl -sL http://www.openssl.org/source/openssl-1.0.1k.tar.gz | tar -xvz
WORKDIR /tmp/openssl-1.0.1k
RUN ./config && make && make install

WORKDIR /tmp
RUN curl -sL https://github.com/php/php-src/archive/php-7.3.1.tar.gz | tar -xvz
WORKDIR php-src-php-7.3.1
RUN ./buildconf --force && \
    ./configure \
      --prefix=/usr/local/ \
      --with-openssl=/usr/local/ssl \
      --with-curl \
      --with-zlib \
      --enable-pcntl \
      --without-pear && \
    make install

RUN mkdir /tmp/layer
WORKDIR /tmp/layer
RUN curl -sS https://getcomposer.org/installer | /usr/local/bin/php -- --install-dir=/usr/local/bin --filename=composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN composer require guzzlehttp/guzzle

COPY bootstrap /tmp/layer
RUN chmod +x bootstrap

RUN mkdir /tmp/layer/bin && \
    cp /usr/local/bin/php /tmp/layer/bin

RUN mkdir /tmp/layer/src
COPY phpversion.php /tmp/layer/src
COPY phpinfo.php /tmp/layer/src

RUN zip -r runtime.zip bin bootstrap
RUN zip -r vendor.zip vendor
RUN zip -r phpversion.zip src/phpversion.php
RUN zip -r phpinfo.zip src/phpinfo.php
