FROM centos:7
MAINTAINER Jose Fuentes <jfuentes@wtelecom.es>

RUN cp -r /var/lib/rpm /var/lib/rpm_bk
RUN yum -y -q update && \
    rpm -ivh https://yum.puppetlabs.com/puppetlabs-release-el-7.noarch.rpm && \
    yum -y -q install git puppet curl && \
    yum -y clean all && rm -rf /var/lib/yum /var/cache/yum /tmp/*
RUN rm -rf /var/lib/rpm && cp -r /var/lib/rpm_bk /var/lib/rpm


### Inheritors must:
#
# # Use base
# FROM cloudopting/centosbase:7
# # Add puppet modules:
# ADD modules /tmp/modules
# # Add manifest to apply
# ADD images/<nameOfTheImage>/manifest.pp /tmp/manifest.pp
# # Apply manifest
# RUN puppet apply --modulepath=/tmp/modules /tmp/manifest.pp
