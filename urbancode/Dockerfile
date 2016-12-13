FROM java:8-jre
MAINTAINER Sam Newsome

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y default-jdk
RUN apt-get install -y default-jre
#IBM Urbancode Deploy 6.2.2 Multiplatform English Trial
RUN wget https://www15.software.ibm.com/sdfdl/v2/fulfill/CNEM5EN/Xa.2/Xb.aFmQQe8PD7-rdHLZtxPh33CU3V6uHmqw3BQQz6okMOc/Xc.CNEM5EN/URBANCODE_DEPLOY_6.2.2_EN_EVAL.zip/Xd./Xf.LPR.F1AZ/Xg.8911347/Xi.RATLe-UCDeploy-EVAL/XY.regsrvs/XZ.l5oA4JALSRdxoRCnRI3sRw-iSsU/URBANCODE_DEPLOY_6.2.2_EN_EVAL.zip
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server libmysql-java openjdk-8-jdk openjdk-8-jre unzip
RUN unzip URBANCODE_DEPLOY_6.2.2_EN_EVAL.zip

RUN service mysql start\
&& mysql -u root -e "create user 'ibm-ucd'@'localhost' identified by 'password';"\
&& mysql -u root -e "create database uDeploy;"\
&& mysql -u root -e "grant all on uDeploy.* to 'ibm-ucd'@'localhost';"\
&& mysql -u root -e "grant all privileges on uDeploy.* to 'ibm-ucd'@'localhost' with grant option;"\
&& mysql -u root -e "flush privileges;"

ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
COPY ./install.extra.properties /ibm-ucd-install/
WORKDIR /ibm-ucd-install/
RUN cat install.extra.properties >> install.properties &&\
sed -i '/chmod +x "opt\/apache-ant-\${OUR_ANT_VERSION}\/bin\/ant"/ s/$/; sync/' install-server.sh && \
chmod +x install-server.sh; sync
RUN cp /usr/share/java/mysql.jar /ibm-ucd-install/lib/ext
EXPOSE 8443
EXPOSE 8080
RUN service mysql start &&\
./install-server.sh << EOF\
\n\
\n\
EOF

ENTRYPOINT service mysql start && /opt/ibm-ucd/server/bin/server run
