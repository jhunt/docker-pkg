Docker Packaging
================

This repo contains the Dockerfiles for building reusable Docker
containers for building RPM and DPKG packages in cleanroom
(repeatable) environments.

Debian / Ubuntu Images
----------------------

- **debuild/precise** - Ubuntu 12.04 Precise Pangolin (LTS)
- **debuild/trusty** - Ubuntu 14.04 Trusty Tahr (LTS)
- **debuild/vivid** - Ubunut 15.04 Vivid Vervet


CentOS Images
-------------

- **rpmbuild/centos5** - CentOS 5
- **rpmbuild/centos6** - CentOS 6
- **rpmbuild/centos7** - CentOS 7

Building the Images
===================

    ./build && ./push latest [other tags ...]
