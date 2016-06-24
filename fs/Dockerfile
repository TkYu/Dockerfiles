#
# Dockerfile for finalspeed
#

FROM alpine:latest

MAINTAINER fs <d1sm@ip4a.com>

ENV FS_URL http://ccc.xxx/fs.jar
ENV FS_DIR /fs
ENV FS_DEP wget openjdk8-jre libpcap iptables

USER root

RUN \
  mkdir $FS_DIR && \
  cd $FS_DIR && \
  apk update && \
  apk add --update $FS_DEP && \
  wget -O $FS_URL && \
  rm -rf /var/cache/apk/*

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV SERVER_PORT 150

WORKDIR $FS_DIR

EXPOSE $SERVER_PORT
EXPOSE $SERVER_PORT/udp

CMD ["java -Xmx512M -XX:MaxGCPauseMillis=30 -jar fs.jar"]