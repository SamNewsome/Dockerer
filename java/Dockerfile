#
#Java Dockerfile
#
FROM ubuntu
MAINTAINER Sam Newsome
USER root
RUN apt-get update
RUN apt-get install -y wget
RUN  wget --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.tar.gz
RUN apt-get update
RUN mkdir /opt/java
RUN cp jdk-8u111-linux-x64.tar.gz /opt/java

#Install

RUN  echo 'Container complete'

WORKDIR /opt/java/
RUN pwd
RUN tar xvzf jdk-8u111-linux-x64.tar.gz

RUN update-alternatives --install /usr/bin/java java /opt/java/jdk1.8.0_111/bin/java 100
RUN update-alternatives --install /usr/bin/javac javac /opt/java/jdk1.8.0_111/bin/javac 100


