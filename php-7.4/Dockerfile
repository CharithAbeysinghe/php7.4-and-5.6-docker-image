FROM ubuntu:20.04

MAINTAINER  klcp <charithpriyankara@gmail.com>

ENV TZ=Asia/Colombo

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get -y upgrade 
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt-get -y install apache2 curl rsync git openssh-client php7.4 php7.4-zip php7.4-curl libapache2-mod-php7.4 php7.4-mysql php7.4-mbstring php7.4-json php7.4-gd	php7.4-xml

RUN sed -i "s/max_execution_time = 30/max_execution_time = 3600/" /etc/php/7.4/apache2/php.ini
RUN sed -i "s/max_input_time = 60/max_input_time = 600/" /etc/php/7.4/apache2/php.ini
RUN sed -i "s/; max_input_vars = 1000/max_input_vars = 10000/" /etc/php/7.4/apache2/php.ini
RUN sed -i "s/memory_limit = 128M/memory_limit = 512M/" /etc/php/7.4/apache2/php.ini
RUN sed -i "s/post_max_size = 8M/post_max_size = 1024M/" /etc/php/7.4/apache2/php.ini
RUN sed -i "s/upload_max_filesize = 2M/upload_max_filesize = 1024M/" /etc/php/7.4/apache2/php.ini

RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2ensite default-ssl

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

EXPOSE 80

ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf

CMD /usr/sbin/apache2ctl -D FOREGROUND