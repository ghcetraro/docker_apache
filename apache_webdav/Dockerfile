FROM ubuntu:latest
MAINTAINER eltano <ghcetraro@gmail.com>

# Install apache
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install apache2 apache2-utils openssl 

# Enable apache mods.
RUN a2enmod rewrite
RUN a2enmod dav*
RUN a2enmod ldap*
RUN auth_basic
RUN authnz_ldap

# Update the PHP.ini file, enable <? ?> tags and quieten logging.
# RUN sed -i "s/short_open_tag = Off/short_open_tag = On/" /etc/php/7.0/apache2/php.ini
# RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php/7.0/apache2/php.ini

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

RUN rm -frv /etc/apache2/sites-enabled/*
COPY webdav.conf /etc/apache2/sites-enabled/

# Expose apache.
EXPOSE 80 443

# By default start up apache in the foreground, override with /bin/bash for interative.
CMD /usr/sbin/apache2ctl -D FOREGROUND

