FROM centos:6
MAINTAINER James Hunt <docker@jameshunt.us>

RUN yum install -y gcc gcc-c++ \
                   libtool libtool-ltdl \
                   make cmake \
                   automake autoconf \
                   yum-utils rpm-build && \
    yum clean all

ENV DIST=el6
CMD /srv/build
