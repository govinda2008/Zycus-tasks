FROM centos:centos6

MAINTAINER Govinda Idamakanti <tlr.09081984@gmail.com>

# Updates and dependencies
RUN yum -y update && \
    yum install -y \
    bzip2-devel \
    git \
    hostname \
    openssl \
    apr-devel \
    openssl-devel \
    sqlite-devel \
    sudo \
    tar \
    wget \
    gcc \
    zlib-dev

# Install python2.7
RUN yum install -y centos-release-scl && \
    yum install -y python27 && \
    scl enable python27 bash

# Install mongoDB v 2.4 
RUN yum install -y mongodb24 && \
    scl enable mongodb24 bash    

# Install Oracle Java 8
RUN cd /opt/ && \
    wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-x64.tar.gz" && \
    tar xzf jdk-7u79-linux-x64.tar.gz 
    
RUN cd /opt/jdk1.7.0_79/ && \
    alternatives --install /usr/bin/java java /opt/jdk1.7.0_79/bin/java 2 && \
    echo | alternatives --config java  && \
    alternatives --install /usr/bin/jar jar /opt/jdk1.7.0_79/bin/jar 2 && \
    alternatives --install /usr/bin/javac javac /opt/jdk1.7.0_79/bin/javac 2 && \
    alternatives --set jar /opt/jdk1.7.0_79/bin/jar && \
    alternatives --set javac /opt/jdk1.7.0_79/bin/javac

ENV JAVA_HOME=/opt/jdk1.7.0_79
ENV JRE_HOME=/opt/jdk1.7.0_79/jre
ENV PATH=$PATH:/opt/jdk1.7.0_79/bin:/opt/jdk1.7.0_79/jre/bin

# Install Tomcat 7
RUN wget "http://apache.mirrors.spacedump.net/tomcat/tomcat-7/v7.0.73/bin/apache-tomcat-7.0.73.tar.gz" -O apache-tomcat-7.0.73.tar.gz && \
	tar xvzf apache-tomcat-7.0.73.tar.gz && \
    mv apache-tomcat-7.0.73 /usr/local/tomcat7

#Starting services

CMD ["/etc/init.d/mongodb24-mongodb" , "start" ]
CMD ["/usr/local/tomcat7/bin/catalina.sh" , "run"]

# Expose ports for tomcat and mongodb
EXPOSE 7080 8080
EXPOSE 27017 27017

 
