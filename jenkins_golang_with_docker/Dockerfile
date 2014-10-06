FROM centos:latest

MAINTAINER ciela <zektbach@gmail.com>

# yum
RUN yum -y update && \
	yum -y install initscripts wget tar ntp git && \
	yum -y clean all

# Time Zone
RUN echo 'ZONE="Asia/Tokyo"' > /etc/sysconfig/clock && \
	rm -f /etc/localtime && \
	ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
	ntpdate ntp.nict.jp

# java
RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u20-b26/jdk-8u20-linux-x64.rpm && \
	rpm -ihv jdk-8u20-linux-x64.rpm

# Go
RUN wget https://storage.googleapis.com/golang/go1.3.3.linux-amd64.tar.gz && \
	tar -C /usr/local -xzf go1.3.3.linux-amd64.tar.gz
ENV GOROOT /usr/local/go
RUN mkdir /gopath
ENV GOPATH /gopath
ENV PATH $PATH:/usr/local/go/bin
RUN go get github.com/mattn/gom

# jenkins
RUN wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo && \
	rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key && \
	yum -y install jenkins
RUN wget -nv -T 60 -t 3 -P /var/lib/jenkins/plugins \
		https://updates.jenkins-ci.org/latest/ssh-agent.hpi \
		https://updates.jenkins-ci.org/latest/scm-api.hpi \
		https://updates.jenkins-ci.org/latest/github-api.hpi \
		https://updates.jenkins-ci.org/latest/git.hpi \
		https://updates.jenkins-ci.org/latest/git-client.hpi \
		https://updates.jenkins-ci.org/latest/github.hpi  \
		https://updates.jenkins-ci.org/latest/durable-task.hpi \
		https://updates.jenkins-ci.org/latest/docker-plugin.hpi \
		https://updates.jenkins-ci.org/latest/golang.hpi \
		https://updates.jenkins-ci.org/latest/awseb-deployment-plugin.hpi

EXPOSE 8080
CMD ["java", "-DJENKINS_HOME=/var/lib/jenkins", "-jar", "/usr/lib/jenkins/jenkins.war", "--logfile=/var/log/jenkins/jenkins.log"]
