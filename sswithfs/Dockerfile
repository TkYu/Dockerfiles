FROM ubuntu:latest

MAINTAINER ss <shadowsocks@shadowsocks.org>

ENV DEPENDENCIES git-core build-essential wget autoconf libtool libssl-dev
ENV BASEDIR /tmp/shadowsocks-libev
ENV SERVER_PORT 8338

ENV FS_PORT 150
ENV FS_DEPENDENCIES openjdk-8-jre libpcap-dev iptables
ENV FS_BASEDIR /fs/

# Set up building environment
RUN apt-get update \
 && apt-get install -y $DEPENDENCIES

# Get the latest code, build and install
RUN git clone https://github.com/shadowsocks/shadowsocks-libev.git $BASEDIR
WORKDIR $BASEDIR
RUN ./configure \
 && make \
 && make install
RUN apt-get install -y $FS_DEPENDENCIES
RUN mkdir $FS_BASEDIR
WORKDIR $FS_BASEDIR
RUN wget -O fs.jar http://ccc.xxx/fs.jar
# Tear down building environment and delete git repository
WORKDIR /
RUN rm -rf $BASEDIR/shadowsocks-libev\
 && apt-get --purge autoremove -y $DEPENDENCIES\
 $$ apt-get clean -y

# Port in the config file won't take affect. Instead we'll use 8388.
EXPOSE $SERVER_PORT
EXPOSE $SERVER_PORT/udp
EXPOSE $FS_PORT/udp
# Override the host and port in the config file.
ADD entrypoint /
ENTRYPOINT ["/entrypoint"]
CMD ["-h"]
