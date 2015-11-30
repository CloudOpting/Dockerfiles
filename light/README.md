# Light base

This is a very lightweight base built from scratch.

# Use

It uses [busybox](http://www.busybox.net/). You can run any busybox command.

Scripts must be executed by `/bin/busybox sh` or `/bin/busybox ash`(recommended) interpreter.

# Use cases

## Data-only container.

In docker, a volume has to be attached to a container in order to exist. It's a common practice create containers that just "contains" a volume (which can be mounted by other containers). With the standard docker API you could just create the container with the volume without running any process inside. With compose this is not possible, each container has to be created with a process.

This image can be used to create that _data-only container_ with the minimum overload.


This is an example of `docker-compose.yml` using this image for a typical data-only container:

```yaml
db:
  image: mysql
  volumes_from:
    - db-data

db-data:
  image: cloudopting/lightbase
  volume:
    - /var/lib/mysql/data
  command: echo "Data only container created"
```

Note the command `echo "Data only container created"`, this just make docker-compose create the container. In this case, we don't need the container to be running forever, just create it.

That command can also be used to provision some data on the volume running a script to populate it.
