FROM centos:7

# Use vault.centos.org instead of mirrorlist.centos.org, which doesn't exist
# anymore (see https://serverfault.com/a/1161847).
RUN sed -i.bak -e 's/mirror.centos.org/vault.centos.org/g' \
               -e 's/^#.*baseurl=http/baseurl=http/g' \
               -e 's/\$releasever/7.9.2009/g' \
               -e 's/^mirrorlist=http/#mirrorlist=http/g' \
        /etc/yum.repos.d/*.repo \
    && yum update -y

