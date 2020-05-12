FROM centos:7

# Prepare centos 
RUN yum -y update

RUN yum groupinstall "Development Tools" -y
RUN yum -y install centos-release-scl  epel-release
RUN yum -y install devtoolset-7-gcc-c++ yum-utils cmake3 zlib-devel
RUN yum -y install qt5-qtbase-devel qtkeychain-qt5-devel

ADD https://www.sqlite.org/2020/sqlite-autoconf-3310100.tar.gz .
RUN tar -xvzf sqlite-autoconf-3310100.tar.gz
WORKDIR sqlite-autoconf-3310100
RUN ./configure --enable-shared=no --with-pic --prefix=/usr
RUN make install

WORKDIR /
#ADD https://download.owncloud.com/desktop/stable/owncloudclient-2.5.4.11654.tar.xz /
ADD https://download.owncloud.com/desktop/stable/owncloudclient-2.6.1.13407.tar.xz /
RUN tar -xvJf owncloudclient-2.6.1.13407.tar.xz 
#RUN tar -xvJf owncloudclient-2.5.4.11654.tar.xz

#WORKDIR owncloudclient-2.5.4.11654
WORKDIR owncloudclient-2.6.1.13407

# RUN yum-builddep owncloud-client

SHELL [ "/usr/bin/scl", "enable", "devtoolset-7"]

RUN mkdir client-build && cd client-build && cmake3 .. && make -j4


