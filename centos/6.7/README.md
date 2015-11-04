# CentOS 6.7 CloudOpting base

Docker base for CloudOpting platform based on CentOS 6.7

# Use

Write a new _Dockerfile_ based on one of the base images.

## Requisites for inheritors

_Dockerfiles_ based on the base images must be compliant with these rules:

- Reference the base image: `FROM cloudopting/centosbase:6.7`
- Do application specific stuff (if needed)
- Do cleaning (if needed)
- Add puppet related stuff (mandatory if you want to apply a manifest):


```
### Add puppet modules
ADD modules /tmp/modules

### Add manifest to apply
ADD images/<imagename>/manifest.pp /tmp/manifest.pp

### Apply manifest
RUN puppet apply --modulepath=/tmp/modules /tmp/manifest.pp
```

## Example

```Dockerfile
# Use base
FROM cloudopting/centosbase:6.7

# OPTIONAL:

### Specific application stuff
RUN git clone https://github.com/someorg/somerepo
RUN yum -y -q update && yum -y install some-packages

### Cleaning
RUN yum -y clean all && rm -rf /var/lib/yum /var/cache/yum /tmp/*


# MANDATORY IF YOU WANT TO APPLY A PUPPET MANIFEST:
### Add puppet modules
ADD modules /tmp/modules

### Add manifest to apply
ADD images/apache/manifest.pp /tmp/manifest.pp

### Apply manifest
RUN puppet apply --modulepath=/tmp/modules /tmp/manifest.pp
```
