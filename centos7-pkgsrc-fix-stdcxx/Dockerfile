ARG github_repository=actionsh/centos7_containers
ARG pkgsrc_branch=trunk
FROM ghcr.io/${github_repository}/centos7-pkgsrc-${pkgsrc_branch}:latest
RUN set -x; \
    cd /usr/pkgsrc; \
    yum install -y libquadmath; \
    rebuild() { \
        pkgin -y install $(bmake -C */$1 show-depends-dirs USE_PKGSRC_GCC_RUNTIME=yes | sed 's,.*/,,') || return 1; \
        bmake -C */$1 bin-install USE_PKGSRC_GCC_RUNTIME=yes || return 1; \
        if [ -d */$1/work ]; then \
            bmake -C */$1 clean; \
        else \
            bmake -C */$1 deinstall install clean USE_PKGSRC_GCC_RUNTIME=yes; \
        fi; \
    }; \
    rebuild llvm || exit 1; \
    rebuild patchelf || exit 1; \
    bmake -C */cargo-c bin-install clean || exit 1; \
    true

