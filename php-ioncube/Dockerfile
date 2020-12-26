FROM php:7-fpm-alpine

RUN \
	mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
\
	&& apk update \
	&& apk add --no-cache --virtual build-dependencies $PHPIZE_DEPS \
\
	&& pecl install redis \
	&& docker-php-ext-enable redis \
	&& docker-php-ext-install exif \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install opcache \
	&& apk add --update --no-cache libzip-dev zip && docker-php-ext-install zip \
\
	&& apk add --no-cache --virtual build-dependencies autoconf build-base git \
	&& apk add --no-cache imagemagick imagemagick-dev \
	&& git clone https://github.com/Imagick/imagick.git /usr/src/php/ext/imagick \
	&& docker-php-ext-install imagick \
\
	&& apk add --no-cache freetype-dev libjpeg-turbo-dev libpng libpng-dev libwebp-dev libxpm-dev zlib-dev \
	&& docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
	&& docker-php-ext-install gd \
\
	&& curl -fsSL 'https://www.ioncube.com/php-7.4.0-beta-loaders/ioncube_loaders_lin_x86-64_7.4_BETA2.tar.gz' -o ioncube.tar.gz \ 
	&& mkdir -p /tmp/ioncube \
	&& tar -xvvzf ioncube.tar.gz \
	&& mv ioncube_loader_lin_7.4_10.4.0_beta2.so $( php-config --extension-dir ) \
	&& rm -Rf ioncube.tar.gz ioncube \
	&& docker-php-ext-enable ioncube_loader_lin_7.4_10.4.0_beta2 \
\
	&& apk del build-dependencies