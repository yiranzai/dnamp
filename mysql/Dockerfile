FROM mysql:5.7


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

ADD ./conf/my.cnf /etc/mysql/conf.d/my.cnf

ENV TIMEZONE $CONTAINER_TIMEZONE
RUN apt-get -y update \
  && ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime \
  && echo $TIMEZONE > /etc/timezone \
  && chown -R mysql:mysql /var/lib/mysql/ \