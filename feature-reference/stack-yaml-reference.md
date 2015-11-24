# Stack YAML reference
A stack is a collection of services that make up an application in a specific environment. Learn more about stacks [here](https://tutum.freshdesk.com/support/solutions/articles/5000569899-stacks). A **stack file** is a file in YAML format that define one or more services. The default name for this file is `tutum.yml`, although other filenames are supported. 

Below is an example `tutum.yml`:

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
image: drupal
image: tutum/ubuntu-quantal
image: tutum/ubuntu-quantal:latest
image: quay.io/borja/redis
```

For private images:

```
image: REGISTRY/NAMESPACE/IMAGE_NAME:TAG
image: tutum.co/borja/hello:latest
```

## command
Override the default command in the image.

```
command: echo 'Hello World!'
```

## environment
A list of environment variables to be added in the service containers on launch (overriding any image-defined environment variables). You can use either an array or a dictionary.

```
environment:
    PASSWORD: my_password
```

```
environment:
  - PASSWORD=my_password
```

When using the Tutum CLI to create a stack, you can use the environment variables locally defined in your shell to define those in the stack. This is convenient if you don't want to store passwords or any other sensitive information in your stack file:

```
environment:
  - PASSWORD
```

## labels
Add metadata to containers using Docker labels. You can use either an array or a dictionary.

It’s recommended that you use reverse-DNS notation to prevent your labels from conflicting with those used by other software.

```
labels:
  com.example.description: "Accounting webapp"
  com.example.department: "Finance"
  com.example.label-with-empty-value: ""

labels:
  - "com.example.description=Accounting webapp"
  - "com.example.department=Finance"
  - "com.example.label-with-empty-value"
```

## links
Link to another service. Either specify both the service unique name and the link alias (`SERVICE:ALIAS`), or just the service unique name (which will also be used for the alias). If the target service belongs to this stack its service unique name is its service name. If the target service does not belong to any stack its service unique name is its service name. If the target service belongs to another stack its service unique name is its service name plus the service stack name, separated by ".".

```
links:
 - mysql
 - redis:cache
 - amqp.staging:amqp
```
Environment variables will be created for each link that Tutum resolves to the containers IPs of the linked service. More information [here](https://support.tutum.co/support/solutions/articles/5000012181-service-links).

## ports
Expose ports. Either specify both ports (`HOST:CONTAINER`), or just the container port (a random host port will be chosen). `udp` ports can be specified with a `/udp` suffix.

```
ports:
 - "80"
 - "443:443"
 - "500/udp"
 - "4500:4500/udp"
 - "49022:22"
```

## expose
Expose ports without publishing them to the host machine - they'll only be accessible from your nodes in Tutum. `udp` ports can be specified with a `/udp` suffix.

```
expose:
 - "80"
 - "90/udp"
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
Mount all of the volumes from another service by specifying a service unique name. If the target service belongs to this stack its service unique name is its service name. If the target service does not belong to any stack its service unique name is its service name. If the target service belongs to another stack its service unique name is its service name plus the service stack name, separated by ".". Learn more [here](https://tutum.freshdesk.com/support/solutions/articles/5000520731).

```
volumes_from:
 - database
 - mongodb.staging
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

## restart
Whether the containers for this service should be restarted if they stop (default: `no`, possible values: `no`, `on-failure`, `always`).

```
restart: always
```

## autodestroy
Whether the containers for this service should be terminated if they stop (default: `no`, possible values: `no`, `on-success`, `always`).

```
autodestroy: always
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

Whether to start the containers with Docker's privileged flag set or not (default: false).

```
privileged: true
```

## net
Networking mode. Only "bridge" and "host" options are supported for now.

```
net: host
```

## pid
Sets the PID mode to the host PID mode. This turns on sharing between container and the host operating system the PID address space. Containers launched with this (optional) flag will be able to access and manipulate other containers in the bare-metal machine’s namespace and vise-versa.

```
pid: "host"
```

##dns
Custom DNS servers. Can be a single value or a list.

```
dns: 8.8.8.8
dns:
  - 8.8.8.8
  - 9.9.9.9
```

##dns_search
Custom DNS search domains. Can be a single value or a list.

```
dns_search: example.com
dns_search:
  - dc1.example.com
  - dc2.example.com
```

## cap_add, cap_drop
Add or drop container capabilities. See `man 7 capabilities` for a full list.

```
cap_add:
  - ALL
cap_drop:
  - NET_ADMIN
  - SYS_ADMIN
```

## devices
List of device mappings. Uses the same format as the `--device` docker client create option.

```
devices:
  - "/dev/ttyUSB0:/dev/ttyUSB0"
```

## extra_hosts
Add hostname mappings. Use the same values as the docker client `--add-host` parameter.

```
extra_hosts:
  - "somehost:162.242.195.82"
  - "otherhost:50.31.209.229"
```

## security_opt
Override the default labeling scheme for each container.

```
security_opt:
  - label:user:USER
  - label:role:ROLE
```

## cgroup_parent
Specify an optional parent cgroup for the container.

```
cgroup_parent: m-executor-abcd
```

## Single value keys analogous to its `docker run` counterpart
```
working_dir: /app
entrypoint: /app/entrypoint.sh
user: root
hostname: foo
domainname: foo.com
mac_address: 02:42:ac:11:65:43
cpu_shares: 512
cpuset: 0,1
mem_limit: 100000m
privileged: true
read_only: true
stdin_open: true
tty: true
```


## Docker-compose non-supported keys

Tutum.yml has been designed with `docker-compose.yml` in mind to maximize compatibility, but the following keys are not supported: 

```
build
external_links
env_file
```
