FROM php:8.2-fpm-alpine

RUN apk update && apk upgrade

 RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
     php composer-setup.php && \
     php -r "unlink('composer-setup.php');" && \
     mv composer.phar /usr/local/bin/composer;

RUN apk add --no-cache supervisor && \
 apk add --no-cache git && \
 apk add --no-cache autoconf && \
 apk add --no-cache postgresql-client && \
 apk add --no-cache gcc make g++ zlib-dev

# using mlocati/php-extension-installer to simplifiy php extension installation for all php version
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/
RUN install-php-extensions opcache pdo_mysql pcntl zip intl redis

ADD ./custom-php.ini /usr/local/etc/php/conf.d/custom-php.ini
ADD ./custom-php-fpm.conf /usr/local/etc/php-fpm.d/custom-php-fpm.conf

RUN composer self-update
