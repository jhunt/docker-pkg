Ubuntu Vivid Vervet (15.04)
===========================

This docker image can be used to build Debian/Ubuntu packages.

Third-Party Repositories
------------------------

None.

Installed Software
------------------

Aside from the additions to make a baseline kit (sudo, git, etc.), the following software is loaded:

- autoconf / libtool / devscripts
- pkg-config
- debhelper

User Account and Root Access
----------------------------

The `builder` user (UID 1000) is a member of staff and sudo, and has password-less sudo as any user, any group.

Environment Variables
---------------------

Build scripts can make use of the following environment variables:

- **FLAVOR** - will be set to `debuild`
- **OS** - will be set to `ubuntu`
- **DIST** - will be set to `vivid`

Hook / Integration
------------------

When running this container, you will need to provide a `/srv` mountpoint, which must contain, at its root, a `pkg` script that is executable.  The image will execute this build script to perform the actual packaging (including installation of dependencies, running of tests, debuild calls, etc.)

Dockerfile
----------

Here is the Dockerfile used to build this image:

    FROM ubuntu:15.04

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

    ENV FLAVOR=debuild OS=ubuntu DIST=vivid
    CMD /srv/pkg
