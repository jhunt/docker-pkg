FROM ubuntu:15.04
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

ENV DIST=vivid
CMD /srv/build
