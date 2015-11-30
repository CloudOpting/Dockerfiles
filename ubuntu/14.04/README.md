# Ubuntu 14.04 CloudOpting base

Docker base for CloudOpting platform based on Ubuntu 14.04

Available on DockerHub: [cloudopting/ubuntubase:14.04](https://hub.docker.com/r/cloudopting/ubuntubase/)

# Use

Write a new _Dockerfile_ based on one of the base images.

## Requisites for inheritors

_Dockerfiles_ based on the base images must be compliant with these rules:

- Reference the base image: `FROM cloudopting/ubuntubase:14.04`
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
FROM cloudopting/ubuntubase:14.04

# OPTIONAL:

### Specific application stuff
RUN git clone https://github.com/someorg/somerepo
RUN apt-get -yq update && apt-get install -y some-packages

### Cleaning
RUN apt-get clean && rm -rf /var/lib/apt /var/cache/apt/archives/* /tmp/*


# MANDATORY IF YOU WANT TO APPLY A PUPPET MANIFEST:
### Add puppet modules
ADD modules /tmp/modules

### Add manifest to apply
ADD images/apache/manifest.pp /tmp/manifest.pp

### Apply manifest
RUN puppet apply --modulepath=/tmp/modules /tmp/manifest.pp
```
