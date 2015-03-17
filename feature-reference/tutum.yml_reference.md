# Tutum.yml reference

`tutum.yml` is a YAML representation of a collection of services that make up an application in a specific environment.

```
lb:
  image: tutum/haproxy
  links:
    - "web:web"
  ports:
    - "80:80"
  roles:
    - global

web:
  image: tutum/quickstart-python
  links:
    - "redis:redis"
  target_num_containers: 4

redis:
  image: tutum/redis
  environment:
    - REDIS_PASS=password
```

Each key defined in `tutum.yml` will create a service with that name in Tutum. Each service is a dictionary whose possible keys are documented below. The image key is mandatory. Other keys are optional and are analogous to their [Tutum Service API](https://docs.tutum.co/v2/api/#create-a-new-service) counterparts.  

## image

The image used to deploy this service in docker format.

```
image: tutum/ubuntu-quantal
image: tutum/ubuntu-quantal:latest
```

## environment
A list of environment variables to be added in the service containers on launch (overriding any image-defined environment variables). You can use either an array or a dictionary.

```
environment:
    PASSWORD: my_password

environment:
  - PASSWORD=my_password
```

## links
Link to another service. Either specify both the service name and the link alias (`SERVICE:ALIAS`), or just the service name (which will also be used for the alias). External services in the stack can be referred by its service name if it is unique or by its service uuid.

```
links:
 - mysql
 - redis:cache
 - c652342c-3cae-4b27-9285-798f0b348631:amqp
```

Environment variables will be created for each link that Tutum resolves to the containers IPs of the linked service. More information [here](https://support.tutum.co/support/solutions/articles/5000012181-service-links).

## ports
Expose ports. Either specify both ports (`HOST:CONTAINER`), or just the container port (a random host port will be chosen).

```
ports:
 - "80"
 - "443:443"
 - "49022:22"
```

## expose
Expose ports without publishing them to the host machine - they'll only be accessible from your nodes in Tutum. Only the internal port can be specified.

```
expose:
 - "80"
```

## volumes
Mount paths as volumes, optionally specifying a path on the host machine (`HOST:CONTAINER`), or an access mode (`HOST:CONTAINER:ro`).

```
volumes:
 - /etc/mysql
 - /sys:/sys
 - /etc:/etc:ro
```

## volumes_from
Mount all of the volumes from another service. You can refer other services by name or by uuid if they are external to this stack. Learn more [here](https://tutum.freshdesk.com/support/solutions/articles/5000520731).

```
volumes_from:
 - database
 - c652342c-3cae-4b27-9285-798f0b348631
```

## tags
Indicates the [deploy tags](https://tutum.freshdesk.com/support/solutions/articles/5000508859) to select the nodes where containers are created.

```
tags:
	- staging
	- web
```

## target_num_containers
The number of containers to run for this service (default: 1).

```
target_num_containers: 3
```

## autorestart
Whether the containers for this service should be restarted if they stop (default: `off`, possible values: `off`, `on_failure`, `always`).

```
autorestart: always
```

## autodestroy
Whether the containers for this service should be terminated if they stop (default: `off`, possible values: `off`, `on_failure`, `always`).

```
autodestroy: alway'
```

## deployment_strategy
Container distribution among nodes (default: `emptiest_node`, possible values: `emptiest_node`, `high_availability`, `every_node`). Learn more [here](https://support.tutum.co/support/solutions/articles/5000520721).

```
deployment_strategy: high_availability
```

## sequential_deployment
Whether the containers should be launched and scaled in sequence (default: `false`). Learn more [here](https://support.tutum.co/support/solutions/articles/5000012179-service).

```
sequential_deployment: true
```

## roles
A list of Tutum API roles to grant the service. The only supported value is `global`, which creates an environment variable `TUTUM_AUTH` used to authenticate againts Tutum API. Learn more [here](https://support.tutum.co/support/solutions/articles/5000524639-api-roles).

```
roles:
	- global
```

## autoredeploy
Whether to redeploy the containers of the service when its image is updated in Tutum registry (default: `false`). Learn more about the Tutum Private Registry [here](https://support.tutum.co/support/solutions/articles/5000012183-using-tutum-s-private-docker-image-registry).

```
autoredeploy: true
```

## privileged
Whether to start the containers with Docker's `privileged` flag set or not (default: `false`).

```
privileged: true
```

## command & entrypoint
Override the default command or entrypoint defined in the image.

```
command: echo 'Hello World!'
entrypoint: echo 'Hi World!'
```

## cpu_shares & mem_limit
The relative CPU priority and the memory limit of the created containers. See the [Runtime Constraints on CPU and Memory](https://docs.docker.com/reference/run/#runtime-constraints-on-cpu-and-memory) to learn more.

```
cpu_shares: 512
mem_limit: 100000m
```


## Docker-compose non-supported keys

Tutum.yml has been designed with `docker-compose.yml` in mind to maximize compatibility, but the following keys are not supported: 

```
dns
dns_search
working_dir
user
hostname
net
domainname
build
external_links
env_file
cap_add
cap_drop
stdin_open
tty
```