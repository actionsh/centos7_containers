ARG github_repository=actionsh/centos7_containers
FROM ghcr.io/${github_repository}/centos7-pkgsrc-bootstrapped:latest
ARG pkgsrc_branch=trunk

# Prepare for pkgsrc
RUN yum install -y bzip2 cvs ed gcc gcc-c++ git libquadmath m4 openssh-clients psmisc which
RUN echo 'BINPKG_SITES+= https://pkgsrc.smartos.org/packages/Linux/el7/trunk/x86_64' > /usr/pkg/etc/mk.conf.local \
    && echo "MAKE_JOBS=$(nproc)" >> /usr/pkg/etc/mk.conf.local \
    && git clone --single-branch \
          --branch "$(case $pkgsrc_branch in (2*q?) echo pkgsrc-$(echo $pkgsrc_branch|tr q Q) ;; (*) echo $pkgsrc_branch ;; esac)" \
          https://github.com/NetBSD/pkgsrc.git /usr/pkgsrc
