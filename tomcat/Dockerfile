FROM ubuntu
RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y default-jdk
RUN apt-get install -y default-jre
WORKDIR /opt
RUN wget http://mirrors.ukfast.co.uk/sites/ftp.apache.org/tomcat/tomcat-7/v7.0.73/bin/apache-tomcat-7.0.73.tar.gz
RUN ls
RUN tar zxvf apache-tomcat-7.0.73.tar.gz
RUN chmod a+x /opt/apache-tomcat-7.0.73/bin/startup.sh
EXPOSE 8085:8080
ENTRYPOINT /opt/apache-tomcat-7.0.73/bin/startup.sh start && bash

