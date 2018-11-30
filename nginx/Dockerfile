FROM nginx:1.14.0

# COPY ./nginx.conf /etc/nginx/nginx.conf
# COPY ./proxy.conf /etc/nginx/proxy.conf


ARG DEB_CUSTOMIZE_MIRROR=deb.debian.org
ENV DEB_CUSTOMIZE_MIRROR ${DEB_CUSTOMIZE_MIRROR}
RUN if [ ${DEB_CUSTOMIZE_MIRROR} ]; then \
    sed -i "s/deb.debian.org/${DEB_CUSTOMIZE_MIRROR}/g" /etc/apt/sources.list; \
    sed -i "s|security.debian.org/debian-security|${DEB_CUSTOMIZE_MIRROR}/debian-security|g" /etc/apt/sources.list \
    ;fi



# mirror http scheme
ARG HTTPS_MIRROR=false
RUN if [ ${HTTPS_MIRROR} = true ]; then \
    sed -i "s/http:\/\//https:\/\//g" /etc/apt/sources.list \
    ;else \
    sed -i "s/https:\/\//http:\/\//g" /etc/apt/sources.list \
    ;fi

RUN apt-get -y update \