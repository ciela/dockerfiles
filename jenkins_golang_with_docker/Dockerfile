FROM centos:latest

MAINTAINER ciela <zektbach@gmail.com>

# yum
RUN yum -y update && \
	yum -y install wget

# java
RUN wget --no-check-certificate --no-cookies - --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u20-b26/jdk-8u20-linux-x64.rpm && \
	rpm -ihv jdk-8u20-linux-x86.rpm

# jenkins
RUN wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo && \
	rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key && \
	yum -y install jenkins

# Go

# AWS プラグインインストール

CMD ["/usr/local/bin/jenkins"]
