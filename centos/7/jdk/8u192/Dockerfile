## Name			|	Version		|	Source

# CentOS 		|	7 			|	https://hub.docker.com/_/centos
# OracleJDK 	|	8u192		|	https://download.oracle.com/otn-pub/java/jdk/8u192-b12/750e1c8617c5452694857ad95c3ee230/jdk-8u192-linux-x64.tar.gz

FROM local/centos7-systemd:latest

LABEL imagename="local/centos7/jdk8u192"
LABEL maintainer="khromov.igor@gmail.com"

RUN echo 'Installing Oracle JDK 8u192 ...' \
	&& cd /opt \
	&& mkdir jdk \
	&& cd jdk \
	&& wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "https://download.oracle.com/otn-pub/java/jdk/8u192-b12/750e1c8617c5452694857ad95c3ee230/jdk-8u192-linux-x64.tar.gz" \
	&& tar xzf ./jdk-8u192-linux-x64.tar.gz \
	&& ln -s ./jdk1.8.0_192 ./current \
	&& rm -rf /opt/jdk/jdk-8u192-linux-x64.tar.gz \
	&& touch /etc/profile.d/javaenv.sh \
	&& echo "# Oracle JDK" | tee -a /etc/profile.d/javaenv.sh \
	&& echo 'export JAVA_HOME=/opt/jdk/current' | tee -a /etc/profile.d/javaenv.sh \
	&& echo 'export PATH=$PATH:/opt/jdk/current/bin' | tee -a /etc/profile.d/javaenv.sh \
	&& source /etc/profile.d/javaenv.sh