FROM ubuntu:15.04
MAINTAINER James Hunt <docker@jameshunt.us>

RUN apt-get update && \
    apt-get install -y autoconf \
                       pkg-config \
                       debhelper \
                       devscripts \
                       equivs \
                       libtool libtool-bin \
                       sudo \
                       git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN useradd builder -m -G staff,sudo && \
    echo "builder ALL=(ALL:ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    mkdir -p /home/builder/debuild && \
    chown builder /home/builder/debuild
USER builder

ENV FLAVOR=debuild DIST=vivid
CMD /srv/build
