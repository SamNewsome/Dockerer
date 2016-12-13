
# Basics

FROM java
USER root
MAINTAINER Sam Newsome
WORKDIR /opt/
RUN apt-get update
RUN apt-get install -y wget
RUN wget https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-7.2.3-x64.bin
RUN chmod a+x atlassian-jira-software-7.2.3-x64.bin
RUN pwd
COPY ./response.varfile /opt/
RUN /opt/atlassian-jira-software-7.2.3-x64.bin -q -varfile /opt/response.varfile
EXPOSE 8081
ENTRYPOINT service jira start && bash
