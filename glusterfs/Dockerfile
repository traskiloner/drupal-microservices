#Container OS
FROM debian:stretch

#Maintaner of Dockerfile
MAINTAINER "Alberto Andrades Gil" "alberto.andrades.gil@gmail.com"

#Update and upgrade base system
RUN apt update && apt upgrade -y && apt dist-upgrade -y

#Install Apache Web Server and PHP dependencies
RUN apt install glusterfs-server -y

#Copy script setup volume to share
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
EXPOSE 111 24007 24008 38465 38466 38467 49152

#Memory limit
CMD ["-m","512"]

#User to run glusterfs master proccess
USER root

#Entrypoint
ENTRYPOINT ["/docker-entrypoint"]
