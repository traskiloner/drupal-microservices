#Container OS
FROM debian:stretch

#Maintaner of Dockerfile
MAINTAINER "Alberto Andrades Gil" "alberto.andrades.gil@gmail.com"

#Update and upgrade base system"
RUN apt update && apt upgrade -y && apt dist-upgrade -y

#Install PHP7, FastCGI Process Manager and PHP dependencies
RUN apt install php7.0 php7.0-fpm php7.0-gd php7.0-memcached php7.0-curl php7.0-mysql \
    php7.0-mysqlnd php7.0-intl php-pear php7.0-imagick php7.0-imap php7.0-mcrypt \
    php7.0-ps php7.0-pspell php7.0-recode php7.0-snmp php7.0-tidy php7.0-xmlrpc \
    php7.0-xsl php7.0-apcu wget -y

#Copy configuration files
COPY ./conf/www.conf /etc/php/7.0/fpm/pool.d/www.conf
COPY ./conf/docker-entrypoint /docker-entrypoint

RUN chmod +x /docker-entrypoint

#Cleaning container
RUN apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /build && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*

#Port to expose
EXPOSE 9000

#Memory limit
CMD ["-m","512"]

#User to run php7.0-fpm master proccess
USER root

#Entrypoint
ENTRYPOINT ["/docker-entrypoint"]

