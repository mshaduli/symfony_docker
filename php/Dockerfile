FROM php:7.4-fpm

RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip libpng-dev \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip
	
RUN docker-php-ext-install gd

RUN apt install -y libxslt1-dev && \
    docker-php-ext-install xsl && \
    apt-get remove -y libxslt1-dev icu-devtools libicu-dev libxml2-dev && \
    rm -rf /var/lib/apt/lists/*
	
RUN apt update && apt install -y libmcrypt-dev \
	    && pecl install mcrypt-1.0.4 \
	    && docker-php-ext-enable mcrypt
		
RUN apt install -y vim
RUN apt install -y supervisor

WORKDIR /var/www/symfony_docker


RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#RUN curl -sS https://get.symfony.com/cli/installer | bash
#RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony
RUN apt-get install sudo -y
RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash
RUN apt install symfony-cli
RUN git config --global user.email ${GITHUB_EMAIL} \ 
    && git config --global user.name ${GITHUB_NAME}