ARG PHP_VERSION

FROM php:${PHP_VERSION}-fpm

RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
		libzip-dev \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd

RUN mkdir -p /usr/src/php/ext/redis; \
	curl -fsSL https://pecl.php.net/get/redis --ipv4 | tar xvz -C "/usr/src/php/ext/redis" --strip 1; \
	docker-php-ext-install redis;

RUN docker-php-ext-install zip

RUN docker-php-ext-install pdo pdo_mysql mysqli

RUN docker-php-ext-install bcmath 

RUN docker-php-ext-install opcache

RUN apt-get update \
	&& apt-get install -y gnupg2

# install and setup custom extensions
RUN apt-get -qq -y update \
	&& apt-get --no-install-recommends -qq -y install apt-transport-https \
	# mssql odbc driver
	# && rm /etc/apt/trusted.gpg \
	&& curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
	&& curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
	&& apt-get -qq -y update \
	&& ACCEPT_EULA=Y apt-get install -y msodbcsql17 odbcinst=2.3.7 odbcinst1debian2=2.3.7 unixodbc-dev=2.3.7 unixodbc=2.3.7 \
	# install and enable extensions
	&& pecl install pdo_sqlsrv-5.10.1 \
	&& docker-php-ext-enable pdo_sqlsrv

# RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
# 	&& curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > /etc/apt/sources.list.d/mssql-release.list \
# 	&& apt-get update \
# 	&& ACCEPT_EULA=Y apt-get install -y msodbcsql17 mssql-tools unixodbc-dev \ 
# 	&& rm -rf /var/lib/apt/lists/*

# RUN docker-php-ext-install pdo_sqlsrv

# RUN docker-php-ext-install sqlsrv
	# ds exif intl opcache \
	# pcntl\ 
	# pdo_sqlsrv\
	# sqlsrv\
	# zip

EXPOSE 9000