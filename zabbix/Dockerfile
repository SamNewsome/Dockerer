FROM ubuntu:14.04
MAINTAINER Sam Newsome

RUN apt-get update
RUN echo "deb http://ppa.launchpad.net/tbfr/zabbix/ubuntu precise main" >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/tbfr/zabbix/ubuntu precise main" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C407E17D5F76A32B
RUN apt-get update
RUN apt-get install -y zabbix-server-mysql php5-mysql zabbix-frontend-php

#Setup MySQL
WORKDIR /usr/share/zabbix-server-mysql/
RUN gunzip *.gz
RUN service mysql start\
&& mysql -u root -e "create user 'zabbix'@'%' identified by '';"\
&& mysql -u root -e "create database zabbix;"\
&& mysql -u root -e "grant all privileges on zabbix.* to 'zabbix'@'%';"\
&& mysql -u root -e "flush privileges;"\
&& mysql -u zabbix zabbix < schema.sql\
&& mysql -u zabbix zabbix < images.sql\
&& mysql -u zabbix zabbix < data.sql

#Setup PHP
RUN sed -i '673s/.*/post_max_size = 16M/' /etc/php5/apache2/php.ini
RUN sed -i '385s/.*/max_execution_time = 300/' /etc/php5/apache2/php.ini
RUN sed -i '395s/.*/max_input_time = 300/' /etc/php5/apache2/php.ini
RUN sed -i '879s/.*/date.timezone = UTC/' /etc/php5/apache2/php.ini

RUN cp /usr/share/doc/zabbix-frontend-php/examples/zabbix.conf.php.example /etc/zabbix/zabbix.conf.php
RUN sed -i '13s/.*/$DB["DATABASE"]= "zabbix";/' /etc/zabbix/zabbix.conf.php
RUN sed -i '13s/.*/$DB["USER"]= "zabbix";/' /etc/zabbix/zabbix.conf.php
RUN sed -i '13s/.*/$DB["PASSWORD"]= "";/' /etc/zabbix/zabbix.conf.php
RUN cp /usr/share/doc/zabbix-frontend-php/examples/apache.conf /etc/apache2/conf-enabled/zabbix.conf

#RUN a2enmod alias
RUN sed -i '11s/.*/ START=yes /' /etc/default/zabbix-server
EXPOSE 8084
ENTRYPOINT service mysql start && service apache2 restart && service zabbix-server start && bash
