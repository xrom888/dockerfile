## Name			|	Version		|	Source
# CentOS 		|	7 			|	https://hub.docker.com/_/centos

FROM centos:7

LABEL imagename="local/centos7-systemd"
LABEL maintainer="khromov.igor@gmail.com"

ENV container docker

# Install basic tools
RUN echo 'Installing wget, tar, nano, telnet, nmap, net-tools ...' \
	&& yum -y install epel-release wget tar nano telnet curl