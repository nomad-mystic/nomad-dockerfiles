# Author Keith Murphy || nomadmystics@gmail.com
# Base Ubuntu Iamge
FROM ubuntu:18.10

# ENV stuff
ENV NODE_VERSION 8.x
ENV PHP_VERSION 7.2
ENV TIMEZONE "America/New_York"
ENV DEBIAN_FRONTEND noninteractive
ENV APACHE_SERVER_NAME www.testing.local

# System Stuff
RUN apt-get update \
    && apt-get install -y wget git curl tzdata \
    && apt-get install -y apt-utils \
    && apt-get update

RUN echo ${TIMEZONE} > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# Node stuff
RUN wget -qO- https://deb.nodesource.com/setup_${NODE_VERSION} \
    && apt-get install -y nodejs \
    && apt-get install -y build-essential \
    && apt-get install -y npm \
    && apt-get update

# Add NPM package stuff
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y yarn

# PHP stuff
RUN apt-get install -y software-properties-common \
    && add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php${PHP_VERSION} \
    && apt-get install -y php${PHP_VERSION}-cli php${PHP_VERSION}-common \
    && apt-get install -y php${PHP_VERSION}-curl php${PHP_VERSION}-gd php${PHP_VERSION}-json \
    && apt-get install -y php${PHP_VERSION}-mbstring php${PHP_VERSION}-intl php${PHP_VERSION}-mysql \
    && apt-get install -y php${PHP_VERSION}-xml php${PHP_VERSION}-zip \
    && apt-get update

# Apache Server stuff
# TODO I need to figure out how to get apache2 to reconize my server name
#RUN sed -i "$ a \ ServerName ${APACHE_SERVER_NAME}" /etc/apache2/apache2.conf \
RUN service apache2 start

#service apache2 start
# Finish stuff
RUN rm -rf /var/lib/apt/lists/*

# expose these ports on the docker virtual network
EXPOSE 80 443 8080
