FROM centos:latest

MAINTAINER ciela <zektbach@gmail.com>

# yum
RUN yum -y update && \
	yum -y install initscripts wget tar ntp && \
	yum -y clean all

# Time Zone
RUN echo 'ZONE="Asia/Tokyo"' > /etc/sysconfig/clock
RUN rm -f /etc/localtime
RUN ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN ntpdate ntp.nict.jp

# java
RUN wget --no-check-certificate --no-cookies - --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u20-b26/jdk-8u20-linux-x64.rpm && \
	rpm -ihv jdk-8u20-linux-x64.rpm

# Go
RUN wget https://storage.googleapis.com/golang/go1.3.3.linux-amd64.tar.gz && \
	tar -C /usr/local -xzf go.release.go1.tar.gz && \
	export PATH=$PATH:/usr/local/go/bin

# jenkins
RUN wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo && \
	rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key && \
	yum -y install jenkins
RUN service jenkins start && sleep 5
RUN wget http://localhost:8080/jnlpJars/jenkins-cli.jar
RUN java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin \
	https://updates.jenkins-ci.org/latest/github.hpi \
	https://updates.jenkins-ci.org/latest/docker.hpi \
	https://updates.jenkins-ci.org/latest/go.hpi \
	https://updates.jenkins-ci.org/latest/awseb-deployment.hpi

EXPOSE 8080
ENTRYPOINT ["tail", "-f", "/var/log/jenkins/jenkins.log"]
