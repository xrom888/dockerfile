## Name			|	Version		|	Source

# CentOS 		|	7 			|	https://hub.docker.com/_/centos
# OracleJDK 	|	8u192		|	https://download.oracle.com/otn-pub/java/jdk/8u192-b12/750e1c8617c5452694857ad95c3ee230/jdk-8u192-linux-x64.tar.gz
# Tomcat		|	9.0.14		|	https://www-eu.apache.org/dist/tomcat/tomcat-9/v9.0.14/bin/apache-tomcat-9.0.14.tar.gz

# To run container with systemctl, user --cap-add SYS_ADMIN
# docker container run --cap-add SYS_ADMIN


FROM local/centos7/jdk8u192:latest

LABEL imagename="local/c7-tomcat:9.0.14"
LABEL maintainer="khromov.igor@gmail.com"

# Install Tomcat 9.0.14
RUN echo 'Installing Tomcat 9.0.14 ...' \
	&& cd /opt \
	&& mkdir tomcat \
	&& cd tomcat \
	&& wget https://www-eu.apache.org/dist/tomcat/tomcat-9/v9.0.14/bin/apache-tomcat-9.0.14.tar.gz \
	&& tar xzf ./apache-tomcat-9.0.14.tar.gz \
	&& rm -rf /opt/tomcat/apache-tomcat-9.0.14.tar.gz

RUN adduser tomcat \
	&& cd /opt/tomcat \
	&& chown -R root:tomcat ./apache-tomcat-9.0.14 \
	&& cd /opt/tomcat/apache-tomcat-9.0.14 \
	&& chmod -R 550 ./conf \
	&& chown -R tomcat:tomcat logs/ temp/ webapps/ work/ \
	&& chmod -R 770 logs/ temp/ webapps/ work/

RUN cd /opt/tomcat \
	&& ln -s ./apache-tomcat-9.0.14 ./current

RUN touch /etc/profile.d/tomcatenv.sh \
	&& echo '# Tomcat' | tee -a /etc/profile.d/tomcatenv.sh \
	&& echo 'export CATALINA_HOME=/opt/tomcat/current' | tee -a /etc/profile.d/tomcatenv.sh \
	&& echo 'export CATALINA_BASE=/opt/tomcat/current' | tee -a /etc/profile.d/tomcatenv.sh \
	&& echo alias tomcat-start=\'runuser -l tomcat bash -c \"/opt/tomcat/current/bin/catalina.sh start\"\' | tee -a /etc/profile.d/tomcatenv.sh \
	&& echo alias tomcat-start-jpda=\'runuser -l tomcat bash -c \"/opt/tomcat/current/bin/catalina.sh jpda start\"\' | tee -a /etc/profile.d/tomcatenv.sh \
	&& echo alias tomcat-stop=\'runuser -l tomcat bash -c \"/opt/tomcat/current/bin/catalina.sh stop 1 -force\"\' | tee -a /etc/profile.d/tomcatenv.sh \
	&& echo "alias tomcat-restart='tomcat-stop && tomcat-start'" | tee -a /etc/profile.d/tomcatenv.sh \
	&& source /etc/profile.d/tomcatenv.sh

RUN cd /opt/tomcat/current \
	&& mkdir pid \
	&& chown root:tomcat ./pid \
	&& chmod 770 ./pid

RUN cd /opt/tomcat/current/bin \
	&& touch setenv.sh \
	&& chown root:tomcat ./setenv.sh \
	&& chmod 750 ./setenv.sh \
	&& echo '#!/bin/bash' | tee -a ./setenv.sh \
	&& echo export CATALINA_PID=\"/opt/tomcat/current/pid/catalina.pid\" | tee -a ./setenv.sh \
	&& echo export JAVA_OPTS=\"-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom\" | tee -a ./setenv.sh

# Install haveged to enfast Tomcat load speed
RUN yum -y install haveged \
	&& systemctl start haveged.service \
	&& systemctl enable haveged.service
