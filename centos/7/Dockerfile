## Name			|	Version		|	Source
# CentOS 		|	7 			|	https://hub.docker.com/_/centos

FROM centos:7

LABEL imagename="local/centos7-systemd"
LABEL maintainer="khromov.igor@gmail.com"

ENV container docker

# Update CentOS
RUN echo 'Updating CentOS ...'
RUN yum -y update

#Add epel repo
RUN yum -y install epel-release

# Install basic tools
RUN echo 'Installing wget, tar, nano, telnet, nmap, net-tools ...'
RUN yum -y install wget	tar nano telnet nmap net-tools curl

# Enable systemctl
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]