FROM java:latest

MAINTAINER ss <shadowsocks@shadowsocks.org>

ENV DEPENDENCIES git-core build-essential wget unzip autoconf libtool libssl-dev
ENV BASEDIR /tmp/shadowsocks-libev
ENV SERVER_PORT 8338

ENV XS_PORT 130
ENV XS_DEPENDENCIES libpcap-dev iptables
ENV XS_BASEDIR /xs/

# Set up building environment
RUN apt-get update \
 && apt-get install -y $DEPENDENCIES

# Get the latest code, build and install
RUN git clone https://github.com/shadowsocks/shadowsocks-libev.git $BASEDIR
WORKDIR $BASEDIR
RUN ./configure \
 && make \
 && make install
RUN apt-get install -y $XS_DEPENDENCIES
RUN mkdir $XS_BASEDIR
WORKDIR $XS_BASEDIR
RUN wget -O xsocks_server.zip http://www.xsocks.me/xsocks/xsocks_server.zip
RUN unzip xsocks_server.zip
# Tear down building environment and delete git repository
WORKDIR /
RUN rm -rf $BASEDIR/shadowsocks-libev\
 && apt-get --purge autoremove -y $DEPENDENCIES\
 && apt-get clean -y

# Port in the config file won't take affect. Instead we'll use 8388.
EXPOSE $SERVER_PORT
EXPOSE $SERVER_PORT/udp
EXPOSE $XS_PORT/udp
# Override the host and port in the config file.
ADD entrypoint /
RUN chmod +x /entrypoint
ENTRYPOINT ["/entrypoint"]
CMD ["-h"]
