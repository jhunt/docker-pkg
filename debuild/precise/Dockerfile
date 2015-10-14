FROM ubuntu:14.04
MAINTAINER James Hunt <docker@jameshunt.us>

RUN apt-get update && apt-get install -y git debhelper devscripts equivs libtool autoconf

ENV DIST=precise
CMD /srv/build
