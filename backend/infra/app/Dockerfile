FROM php:8.2-fpm


ENV TZ=Asia/Tokyo \
    LANG=c.UTF-8 \
    LANGUAGE=ja_JP:ja \
    LC_ALL=en_US.UTF-8 \
    COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer \
    HOME=/app

WORKDIR ${HOME}

COPY --from=composer:2.5.4 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
    apt-get -y install git libicu-dev libonig-dev libzip-dev unzip locales && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    locale-gen en_US.UTF-8 && \
    localedef -f UTF-8 -i en_US en_US.UTF-8 && \
    mkdir /var/run/php-fpm && \
    docker-php-ext-install intl pdo_mysql zip bcmath && \
    composer config -g process-timeout 3600 && \
    composer config -g repos.packagist composer https://packagist.org && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug
