ARG github_repository=actionsh/centos7_containers
FROM ghcr.io/${github_repository}/centos7:latest

# Bootstrap pkgsrc
ENV PATH=/usr/pkg/sbin:/usr/pkg/bin:$PATH
ENV MANPATH=/usr/pkg/man:$MANPATH
RUN set -ex \
    && BOOTSTRAP_TAR="bootstrap-el7-trunk-x86_64-20220718.tar.gz" \
    && BOOTSTRAP_SHA="7ecea7fd3b49259aa7318d8cd72901966ad5329f" \
    && curl -O https://pkgsrc.smartos.org/packages/Linux/bootstrap/${BOOTSTRAP_TAR} \
    && echo "${BOOTSTRAP_SHA}  ${BOOTSTRAP_TAR}" >check-shasum \
    && sha1sum -c check-shasum \
    && tar -zxpvf ${BOOTSTRAP_TAR} -C / \
    && rm "${BOOTSTRAP_TAR}" \
    && pkgin -y update \
    && cp -p /usr/pkg/lib/lib{ssl,crypto}.so* ~ \
    && LD_LIBRARY_PATH=$HOME pkg_add -U openssl pkg_install pkgin \
    && rm ~/lib{ssl,crypto}.so* \
    && { pkgin -yf full-upgrade || cat /var/db/pkgin/pkg_install-err.log; } \
    && sed -i.bak -e 's/^VERIFIED_INSTALLATION=always/#&/' /usr/pkg/etc/pkg_install.conf
