#Container OS
FROM debian:stretch

#Maintaner of Dockerfile
MAINTAINER "Alberto Andrades Gil" "alberto.andrades.gil@gmail.com"

#Update and upgrade base system
RUN apt update && apt upgrade -y && apt dist-upgrade -y

#Install Apache Web Server and PHP dependencies
RUN apt install apache2 libapache2-mod-fastcgi wget unzip

#Copy configuration files
-- COPY ./conf/
COPY ./conf/drupal.conf /etc/apache2/sites-available

#Setup web server
RUN a2dissite 000-default && a2ensite drupal

#Cleaning container
RUN apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /build && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*

#Port to expose
EXPOSE 443

#Memory limit
CMD ["-m","512"]

#User to run apache master proccess
USER root

#Entrypoint
ENTRYPOINT ["/docker-entrypoint"]

