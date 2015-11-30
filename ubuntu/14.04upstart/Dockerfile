FROM ubuntu-upstart:14.04
MAINTAINER Jose Fuentes <jfuentes@wtelecom.es>

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get -yqq update && \
    apt-get -yqq remove console-setup ifupdown geoip-database && \
    apt-get -yqq --no-install-recommends install puppet curl tar && \
    apt-get clean && rm -rf /var/lib/apt /var/cache/apt/archives/* /tmp/* /var/tmp/*


### Inheritors must:
#
# # Use base
# FROM cloudopting/ubuntubase:14.04
# # Add puppet modules:
# ADD modules /tmp/modules
# # Add manifest to apply
# ADD images/<nameOfTheImage>/manifest.pp /tmp/manifest.pp
# # Apply manifest
# RUN puppet apply --modulepath=/tmp/modules /tmp/manifest.pp
