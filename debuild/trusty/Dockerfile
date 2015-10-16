FROM ubuntu:14.04
MAINTAINER James Hunt <docker@jameshunt.us>

RUN apt-get update && \
    apt-get install -y autoconf \
                       debhelper \
                       devscripts \
                       equivs \
                       libtool \
                       git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV DIST=trusty
CMD /srv/build
