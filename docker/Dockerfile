FROM ubuntu:16.04
MAINTAINER joblocal GmbH "produktentwicklung@joblocal.de"

RUN ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime && echo "Europe/Berlin" > /etc/timezone \
  && apt-get update \
  && apt-get -y --no-install-recommends install \
    locales \
  && apt-get -y --no-install-recommends install \
    wget \
    ca-certificates \
    software-properties-common \
		python-software-properties \
  && locale-gen de_DE de_DE.utf8 \
	&& LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php -y \
  \
	&& apt-get update \
	&& apt-get -y --no-install-recommends install \
		ghostscript \
		poppler-utils \
		jq \
		ca-certificates \
		runit \
		nginx \
		clamdscan \
		php7.0-fpm \
		php7.0-cli \
		php7.0-mcrypt \
		php7.0-curl \
		php7.0-intl \
		php7.0-gd \
		php7.0-mysql \
		php7.0-mbstring \
		php7.0-xml \
		php7.0-zip \
		php-apcu \
		php-imagick \
		php-xdebug \
	&& phpenmod mcrypt \
	&& phpdismod xdebug \
	&& apt-get -y autoremove \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
	&& usermod -u 1000 www-data \
  \
 	# forward request and error logs to docker log collector
 	&& ln -sf /dev/stdout /var/log/nginx/access.log \
 	&& ln -sf /dev/stderr /var/log/nginx/error.log

WORKDIR /var/www

VOLUME ["/var/www"]

EXPOSE 80

COPY ./rootfs /

RUN phpenmod memcached solr

CMD ["/usr/bin/runsvdir", "-P", "/etc/service"]
