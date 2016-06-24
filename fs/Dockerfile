#
# Dockerfile for finalspeed
#

FROM cantara/alpine-openjdk-jdk8:latest

MAINTAINER fs <d1sm@ip4a.com>

ENV FS_URL http://ccc.xxx/fs.jar
ENV FS_DIR /fs
ENV FS_DEP wget libpcap iptables

USER root

RUN \
  mkdir $FS_DIR && \
  cd $FS_DIR && \
  apk update && \
  apk add --update $FS_DEP && \
  wget $FS_URL && \
  rm -rf /var/cache/apk/*

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk

ENV SERVER_PORT 150

WORKDIR $FS_DIR

EXPOSE $SERVER_PORT
EXPOSE $SERVER_PORT/udp

CMD ["/usr/lib/jvm/java-1.8-openjdk/bin/java -Xmx512M -XX:MaxGCPauseMillis=30 -jar fs.jar"]