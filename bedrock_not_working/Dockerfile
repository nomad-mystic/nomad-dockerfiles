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
    && apt-get install -y wget git curl tzdata unzip \
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
    && apt-get install -y php-cli php-mbstring \

# Wordpress stuff
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp \
    && apt-get update

# Composer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
    && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
    # Make sure we're installing what we think we're installing!
    && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
    && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot \
    && rm -f /tmp/composer-setup.*

# Apache Server stuff
# @TODO I need to figure out how to get apache2 to reconize my server name
#RUN sed -i "$ a \ ServerName ${APACHE_SERVER_NAME}" /etc/apache2/apache2.conf \
RUN service apache2 start

# DB stuff

#service apache2 start
# Finish stuff
RUN rm -rf /var/lib/apt/lists/*

# Connect local
#VOLUME /var/www/html

# expose these ports on the docker virtual network
EXPOSE 80 443 8080
