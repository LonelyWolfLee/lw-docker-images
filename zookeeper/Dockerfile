FROM openjdk:11

MAINTAINER LonelyWolfLee

ENV ZOOKEEPER_VERSION 3.6.0
ENV ZK_NAME apache-zookeeper-${ZOOKEEPER_VERSION}
ENV ZK_HOME /opt/${ZK_NAME}

#Download Zookeeper
RUN wget -q http://mirror.vorboss.net/apache/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/${ZK_NAME}.tar.gz && \
wget -q https://downloads.apache.org/zookeeper/KEYS && \
wget -q https://downloads.apache.org/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/${ZK_NAME}.tar.gz.asc

#Verify download
RUN gpg --import KEYS && \
gpg --verify ${ZK_NAME}.tar.gz.asc ${ZK_NAME}.tar.gz

#Install
RUN tar -xzf ${ZK_NAME}.tar.gz -C /opt

#Configure
RUN mv ${ZK_HOME}/conf/zoo_sample.cfg ${ZK_HOME}/conf/zoo.cfg
RUN sed  -i "s|/tmp/zookeeper|$ZK_HOME/data|g" $ZK_HOME/conf/zoo.cfg; mkdir $ZK_HOME/data

ADD zookeeper-start.sh /usr/bin/zookeeper-start.sh 
EXPOSE 2181 2888 3888

WORKDIR ${ZK_HOME}
VOLUME ["${ZK_HOME}/conf", "${ZK_HOME}/data"]

ENTRYPOINT /usr/sbin/sshd && bash /usr/bin/zookeeper-start.sh