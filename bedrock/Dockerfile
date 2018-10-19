
# Author Keith Murphy || nomadmystics@gmail.com
# Base Ubuntu Iamge
FROM ubuntu:18.10

# Basic ENV
ENV NODE_VERSION 8.x
ENV PHP_VERSION 7.2

RUN apt-get update \
    	&& apt-get install -y wget git \
    	&& apt-get update \
    	&& wget -qO- https://deb.nodesource.com/setup_8.x \
    	&& apt-get install -y nodejs \
    	&& apt-get install -y build-essential \
#    	&& apt-get update
#    	&& apt-get install -y python-software-properties \
#        && add-apt-repository ppa:ondrej/php \
#        && apt-get update \
#        && apt-get install -y php7.2
        && rm -rf /var/lib/apt/lists/*

EXPOSE 80 443 8080
# expose these ports on the docker virtual network