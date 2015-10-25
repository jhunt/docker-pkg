FROM centos:5
MAINTAINER James Hunt <docker@jameshunt.us>

RUN yum install -y curl && \
      curl -LO http://rpmforge.sw.be/redhat/el5/en/x86_64/rpmforge/RPMS/rpmforge-release-0.5.3-1.el5.rf.x86_64.rpm && \
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

ENV FLAVOR=rpmbuild DIST=el5
CMD /srv/build
