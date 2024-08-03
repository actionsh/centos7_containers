ARG github_repository=actionsh/centos7_containers
ARG pkgsrc_branch=trunk
FROM ghcr.io/${github_repository}/centos7-pkgsrc-${pkgsrc_branch}-fix-stdcxx:latest
COPY pkgsrc-*.patch /root/
RUN <<EOF
set -ex
cd /usr/pkgsrc
yum install -y patch which
patch -p0 < /root/pkgsrc-centos7-openal-soft.patch
patch -p0 < /root/pkgsrc-centos7-tdb.patch
bmake -C */qt5-qtbase bin-install clean
bmake -C */qt5-qtdeclarative bin-install clean
bmake -C */qt5-qtimageformats bin-install clean
bmake -C */qt5-qtsvg bin-install clean
bmake -C */qt5-qttools bin-install clean
bmake -C */qt5-qtwayland bin-install clean
pkgin list
EOF
