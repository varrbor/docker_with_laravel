FROM php:7.2-fpm


# Possible values for ext-name:
# bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp hash iconv imap interbase intl json ldap mbstring mcrypt mysqli oci8 
# odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell readline recode reflection session shmop 
# simplexml snmp soap sockets spl standard sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zip



RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng-dev \
		libbz2-dev \
        libcurl4-gnutls-dev \
		libmagickcore-dev \
		libmagickwand-dev \
		git \		
	&& docker-php-ext-install -j$(nproc) bz2 exif gettext pdo_mysql mysqli opcache soap zip \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
        && docker-php-ext-configure curl --with-curl=/usr/local/lib \ 
        && docker-php-ext-install curl
	
RUN pecl install redis-4.1.1 \
	&& pecl install xdebug-2.6.1 \
	&& pecl install imagick-3.4.3 \
	&& docker-php-ext-enable redis imagick xdebug	
	

RUN  apt-get install -y supervisor	
	
	
WORKDIR /opt

RUN git clone https://github.com/longxinH/xhprof.git ./xhprof
	
WORKDIR /opt/xhprof/extension/
RUN /usr/local/bin/phpize
RUN ./configure --with-php-config=/usr/local/bin/php-config
RUN make &&  make install
	
ADD ./conf  /usr/local/etc	

WORKDIR /app
	
EXPOSE 9070	
	
CMD ["/usr/local/sbin/php-fpm","--nodaemonize"]	
