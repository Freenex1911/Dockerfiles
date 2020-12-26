FROM php:7-fpm-alpine

RUN \
	mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
\
	&& apk update \
	&& apk add --no-cache --virtual build-dependencies $PHPIZE_DEPS \
\
	&& pecl install redis \
	&& docker-php-ext-enable redis \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install pdo_mysql \
\
	&& apk add --no-cache --virtual build-dependencies autoconf build-base pkgconfig \
	&& apk add --no-cache imagemagick imagemagick-dev \
	&& pecl install imagick \
	&& docker-php-ext-enable imagick \
\
	&& apk del build-dependencies