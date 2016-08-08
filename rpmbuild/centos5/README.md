CentOS 5.0
==========

This docker image can be used to build RPM packages.

Third-Party Repositories
------------------------

RPMForge EL5 x86-64

Installed Software
------------------

Aside from the additions to make a baseline kit (sudo, git, etc.), the following software is loaded:

- autoconf / libtool / devscripts
- pkgconfig
- yum-utils
- rpm-build

User Account and Root Access
----------------------------

The `builder` user (UID 1000) is a member of users and wheel, and has password-less sudo as any user, any group.

Environment Variables
---------------------

Build scripts can make use of the following environment variables:

- **FLAVOR** - will be set to `rpmbuild`
- **OS** - will be set to `centos`
- **DIST** - will be set to `el5`

Hook / Integration
------------------

When running this container, you will need to provide a `/srv` mountpoint, which must contain, at its root, a `pkg` script that is executable.  The image will execute this build script to perform the actual packaging (including installation of dependencies, running of tests, debuild calls, etc.)

RPMs will be built in `/home/builder/rpm`, which should contain source archives, patches and built RPM/SRPM files.

Dockerfile
----------

Here is the Dockerfile used to build this image:

    FROM centos:5

    RUN yum install -y curl && \
          curl -LO http://repoforge.mirror.constant.com/redhat/el5/en/x86_64/rpmforge/RPMS/rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm && \
          rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt && \
          rpm -i rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm && \
          rm -f rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm && \
        yum install -y gcc gcc-c++ \
                       libtool libtool-ltdl \
                       make cmake \
                       git \
                       pkgconfig \
                       sudo \
                       automake autoconf \
                       yum-utils rpm-build && \
        yum clean all

    RUN useradd builder -u 1000 -m -G users,wheel && \
        echo "builder ALL=(ALL:ALL) NOPASSWD:ALL" >> /etc/sudoers && \
        echo "# macros"                      >  /home/builder/.rpmmacros && \
        echo "%_topdir    /home/builder/rpm" >> /home/builder/.rpmmacros && \
        echo "%_sourcedir %{_topdir}"        >> /home/builder/.rpmmacros && \
        echo "%_builddir  %{_topdir}"        >> /home/builder/.rpmmacros && \
        echo "%_specdir   %{_topdir}"        >> /home/builder/.rpmmacros && \
        echo "%_rpmdir    %{_topdir}"        >> /home/builder/.rpmmacros && \
        echo "%_srcrpmdir %{_topdir}"        >> /home/builder/.rpmmacros && \
        mkdir /home/builder/rpm && \
        chown -R builder /home/builder
    USER builder

    ENV FLAVOR=rpmbuild OS=centos DIST=el5
    CMD /srv/pkg
