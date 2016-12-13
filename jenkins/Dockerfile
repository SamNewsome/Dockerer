


#Jenkins install
FROM java
USER root
MAINTAINER Sam Newsome
RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y default-jre
RUN apt-get install -y default-jdk
RUN apt-get update
RUN apt-get remove -y default-jre default-jdk
RUN apt-get update
RUN apt-get install -y default-jre default-jdk
RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | apt-key add -
RUN sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
RUN apt-get update
RUN apt-get install -y jenkins
ENTRYPOINT service jenkins start && bash




