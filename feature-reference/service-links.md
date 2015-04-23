Tutum provides two ways to perform service discovery:

* Via **service links**, which are based on Docker's [container links](http://docs.docker.com/userguide/dockerlinks/)
* Using service and container names directly as **hostnames**

Because all containers on a user account are connected to each other automatically via an [overlay network](http://blog.tutum.co/2015/03/03/introducing-overlay-networking-for-containers-and-dynamic-links-in-tutum/) which works across hosts, each container has a local IP (on the `10.7.0.0/16` VLAN) that is reachable from any other container. This also means that all ports are available without port mapping using these IPs, even if they are not exposed in the container.

Tutum maintains a DNS service which is used automatically by all containers to resolve hostnames as described in this document.


# Using links for service discovery

Tutum's service linking capabilities have been modeled after Docker's own [Container Links](http://docs.docker.com/userguide/dockerlinks/). It provides a basic service discovery functionality. Linking a "client" service to a "server" service automatically configures the "client" service with the following:

* Sets a group of environment variables with information about the exposed ports of the "server" service: IP address, port and protocol
* All of the "server" service environment variables are replicated to the "client" service with an `ENV_` prefix
* A DNS hostname is added that resolves to the "server" service IP address.


## Service link example

![](https://s.tutum.co/support/images/service-links-diagram.png)

Imagine that you are running a web service (`my-web-app`) with 2 containers (`my-web-app-1` and `my-web-app-2`). You now want to launch a proxy service (`my-proxy`) with one container (`my-proxy-1`) that will balance HTTP traffic to each of the containers in your `my-web-app` application, with a link name of `web`.


### DNS hostnames

In the example above, the `my-proxy` containers will have the following hostnames available:

Hostname | Value
- | -
`web` | `A 172.16.0.5 172.16.0.6`
`web-1` | `A 172.16.0.5`
`web-2` | `A 172.16.0.6`

The recommended way for the `my-proxy` service to connect to the `my-web-app` service containers is by using these hostnames, as they will be updated at runtime should the `my-web-app` service scale up or down.

There's no need for `SRV` records, as all ports exposed in the server containers are reachable on those IPs without mapping.

If the `my-web-app` service is redeployed, IPs will be reused, even if containers end up in different nodes. This is thanks to the private overlay network we set up between nodes. Also, if `my-web-app` is scaled up, the new hostname `web-3` will automatically resolve to the new IP of the container, and the hostname `web` will be updated as well.


### Environment variables

These are the environment variables that would be set in your proxy containers:
                                                                                                                                                                                                                                                                                                                                                                              
Name | Value
- | -
WEB_1_PORT | `tcp://172.16.0.5:80`
WEB_1_PORT_80_TCP | `tcp://172.16.0.5:80`
WEB_1_PORT_80_TCP_ADDR | `172.16.0.5`
WEB_1_PORT_80_TCP_PORT | `80`
WEB_1_PORT_80_TCP_PROTO | `tcp`
WEB_2_PORT | `tcp://172.16.0.6:80`
WEB_2_PORT_80_TCP | `tcp://172.16.0.6:80`
WEB_2_PORT_80_TCP_ADDR | `172.16.0.6`
WEB_2_PORT_80_TCP_PORT | `80`
WEB_2_PORT_80_TCP_PROTO | `tcp`

Your proxy application can now use these environment variables to configure itself on startup and start balancing traffic between the two containers of `my-web-app`.


### Cascading environment variables

If we had launched our `my-web-app` service with an environment variable of `WEBROOT=/login` for example, the following environment variables will be available in the proxy containers:

Name | Value
- | -
WEB_1_ENV_WEBROOT | `/login`
WEB_2_ENV_WEBROOT | `/login`

This enables your "client" service to be able to read configuration information from your "server" service, such as usernames and passwords, for simplified configuration.


### Tutum specific environment variables

Apart from the standard Docker-like environment variables, Tutum will also set some special environment variables to enable containers to self-configure.

In the example above, you will also find the following environment variables in the `my-proxy` containers:

Name | Value
- | -
WEB_TUTUM_API_URL | `https://dashboard.tutum.co/api/v1/service/3b5fbc69-151c-4f08-9164-a4ff988689ff/`
TUTUM_SERVICE_API_URL | `https://dashboard.tutum.co/api/v1/service/651b58c47-479a-4108-b044-aaa274ef6455/`
TUTUM_CONTAINER_API_URL | `https://dashboard.tutum.co/api/v1/container/20ae2cff-44c0-4955-8fbe-ac5841d1286f/`
TUTUM_CONTAINER_FQDN | `my-proxy-1.username.cont.tutum.io`
TUTUM_CONTAINER_HOSTNAME | `my-proxy-1`
TUTUM_SERVICE_FQDN | `my-proxy.username.svc.tutum.io`
TUTUM_SERVICE_HOSTNAME | `my-proxy`
TUTUM_NODE_FQDN | `d292ef36-username.node.tutum.io`
TUTUM_NODE_HOSTNAME | `d292ef36-username`

Where:

* `WEB_TUTUM_API_URL` is the Tutum API resource URI of the linked service. Note that we use the link name as the environment variable key prefix.
* `TUTUM_SERVICE_API_URL` is the Tutum API resource URI of the service of the container.
* `TUTUM_CONTAINER_API_URL` is the Tutum API resource URI of the container itself.
* `TUTUM_CONTAINER_HOSTNAME` and `TUTUM_CONTAINER_FQDN` are the external hostname and FQDN of the container itself.
* `TUTUM_SERVICE_HOSTNAME` and `TUTUM_SERVICE_FQDN` are the external hostname and FQDN of the service to which the container belongs.
* `TUTUM_NODE_HOSTNAME` and `TUTUM_NODE_FQDN` are the external hostname and FQDN of the node where the container is running.

These environment variables are also "cascaded" to linked containers.

If you provide API access to your service, you can use the generated token (stored in `TUTUM_AUTH`) to access these API URLs to gather information or automate operations, such as scaling.


# Using service and container names as hostnames

We provide a simple way to connect any container on any stack to any other container on your account without having to create service links.


## Discovering containers on the same service or stack

A container can always discover other containers on the same stack using the **container name** as hostname. This includes containers of the same service.

For example, a container `webapp-1` in the service `webapp` can connect to the container `db-1` of the service `db` by just using `db-1` as hostname. It can also connect to `webapp-2` by using `webapp-2` as hostname. Our DNS service (which is configured automatically) will resolve to the appropiate local IP (on the overlay network), even if the container in question is on a different host.

A container `proxy-1` on the same stack could discover all `webapp` containers by using the **service name** `webapp` as hostname. It will resolve as an `A` [round-robin](http://en.wikipedia.org/wiki/Round-robin_DNS) record listing all IPs of all containers on the service `webapp`.


## Discovering containers without stack

In this case, just use the service or container name as hostname. If the container making the query is on a stack and there is a match on the same stack, it will take precedence over the service/container without stack.


## Discovering containers on another stack

To discover a service or a container on another stack, just append `.<stack_name>` to the service or container name. For example, if `webapp-1` on the stack `production` needs to access container `db-1` on the stack `common`, it could use the hostname `db-1.common` which will resolve to the appropiate IP.


