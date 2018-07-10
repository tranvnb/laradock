#FROM webdevops/apache:ubuntu-16.04
FROM webdevops/php-apache-dev:5.6

LABEL maintainer="Eric Pfeiffer <computerfr33k@users.noreply.github.com>"

ARG PHP_UPSTREAM_CONTAINER=php-fpm56
ARG PHP_UPSTREAM_PORT=9000
ARG PHP_UPSTREAM_TIMEOUT=60
ARG DOCUMENT_ROOT=/var/www/

ENV WEB_PHP_SOCKET=${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}

ENV WEB_DOCUMENT_ROOT=${DOCUMENT_ROOT}

ENV WEB_PHP_TIMEOUT=${PHP_UPSTREAM_TIMEOUT}

EXPOSE 80 443

WORKDIR /var/www/

#COPY vhost.conf /etc/apache2/sites-enabled/vhost.conf
#COPY vhost.conf /opt/docker/etc/httpd/vhost.common.d/vhost.conf
COPY sites/*.conf /etc/apache2/sites-enabled/

RUN apt-get update
RUN apt-get install vim -y
RUN a2enmod rewrite
RUN a2enmod headers
#RUN service apache2 restart
#RUN /etc/init.d/apache2 reload

ENTRYPOINT ["/opt/docker/bin/entrypoint.sh"]

CMD ["supervisord"]
