#Container OS
FROM debian:stretch

#Maintaner of Dockerfile
MAINTAINER "Alberto Andrades Gil" "alberto.andrades.gil@gmail.com"

#Update and upgrade base system
RUN apt update && apt upgrade -y && apt dist-upgrade -y

#Install Varnish Cache Server
RUN apt install varnish dnsutils -y

#Copy configuration files
COPY ./conf/docker-entrypoint /docker-entrypoint
COPY ./conf/default.vcl /etc/varnish/default.vcl
RUN chmod u+x /docker-entrypoint

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

#User to run Varnish master proccess
USER root

#Entrypoint configuration
ENTRYPOINT ["/docker-entrypoint"]
