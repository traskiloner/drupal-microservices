#Container OS
FROM debian:stretch

#Maintaner of Dockerfile
MAINTAINER "Alberto Andrades Gil" "alberto.andrades.gil@gmail.com"

#Update and upgrade base system
RUN apt update && apt upgrade -y && apt dist-upgrade -y

#Install Apache Web Server and PHP dependencies
RUN apt install apache2 libapache2-mod-fcgid wget -y

#Copy configuration files
COPY ./conf/php7.0-fpm.conf /etc/apache2/conf-available/
COPY ./conf/drupal.conf /etc/apache2/sites-available/

#Setup web server
RUN a2enmod fcgid actions alias && a2enconf php7.0-fpm && a2dissite 000-default && a2ensite drupal

#Download CMS Drupal 8
RUN wget https://ftp.drupal.org/files/projects/drupal-8.3.2.tar.gz && \
    tar -zxf drupal-8.3.2.tar.gz && \
    mv drupal-8.3.2 /var/www/drupal && \
    rm -r drupal-8.3.2.tar.gz /var/www/html && \
    chown -R www-data:www-data /var/www/drupal

#Cleaning container
RUN apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /build && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*

#Port to expose
EXPOSE 80

#Memory limit
CMD ["-m","512"]

#User to run apache master proccess
USER root

#Run Apache Proccess
CMD ["apache2ctl","-D","FOREGROUND"]

