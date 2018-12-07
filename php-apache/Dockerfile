FROM php:7.2-apache


ARG DEB_CUSTOMIZE_MIRROR
RUN if [ ${DEB_CUSTOMIZE_MIRROR} ]; then \
    sed -i "s/deb.debian.org/${DEB_CUSTOMIZE_MIRROR}/g" /etc/apt/sources.list; \
    sed -i "s|security.debian.org/debian-security|${DEB_CUSTOMIZE_MIRROR}/debian-security|g" /etc/apt/sources.list \
    ;fi

ARG HTTPS_MIRROR=false
RUN if [ ${HTTPS_MIRROR} = true ]; then \
    sed -i "s/http:\/\//https:\/\//g" /etc/apt/sources.list \
    ;else \
    sed -i "s/https:\/\//http:\/\//g" /etc/apt/sources.list \
    ;fi

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer
#COPY composer.phar /usr/bin/composer

# mirror http scheme


RUN apt-get -y update \
    && apt-get -y install supervisor \
    && apt-get -y install zlib1g-dev \
    && useradd -M -s"/sbin/nologin" -U www \
    && chown -R www:www /var/www/html/ \
    && docker-php-ext-install bcmath pdo_mysql zip
# && a2ensite test.cn \