Tutum's service linking capabilities have been modeled after Docker's own [Container Links](http://docs.docker.com/userguide/dockerlinks/). It serves two purposes:

* Creates secure network links between linked containers across different hosts
* Provides a basic service discovery functionality

Linking a "client" service to a "server" service automatically configures the "client" service with the following:

* Sets a group of environment variables with information about the exposed ports of the "server" service: IP address, port and protocol
* All of the "client" service environment variables are replicated to the "server" service with an `ENV_` prefix
* A DNS hostname is added that resolves to the "server" service IP address

It's better explained with an example.


## Real world example

![](https://s.tutum.co/support/images/service-links-diagram.png)

Let's say that you are running a web service (`my-web-app`) with 2 containers (`my-web-app-1` and `my-web-app-2`). You now want to launch a proxy service (`my-proxy`) with one container (`my-proxy-1`) that will balance HTTP traffic to each of the containers in your `my-web-app` application, with a link name of `web`.


### DNS hostnames

In the example above, the `my-proxy` containers will also have the following hostnames available:

Hostname | Value
- | -
`web` | `A 172.16.0.5 172.16.0.6`
`web-1` | `A 172.16.0.5`
`web-2` | `A 172.16.0.6`

The recommended way for the `my-proxy` service to connect to the `my-web-app` service contaiers is by using these hostnames, as they can be updated at runtime.

There's no need for `SRV` records, as all ports exposed in the server containers are reachable on those IPs without mapping.

If the `my-web-app` service is redeployed, these hostnames will automatically resolve to the new IPs if they have changed. Also, if `my-web-app` is scaled up, the new hostname `web-3` will automatically resolve to the new IP of the container.


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
TUTUM_CONTAINER_HOSTNAME | `my-proxy-1.admin.cont.tutum.io`

Where:

* `WEB_TUTUM_API_URL` is the Tutum API resource URI of the linked service. Note that we use the link name as the environment variable key prefix.
* `TUTUM_SERVICE_API_URL` is the Tutum API resource URI of the service of the container.
* `TUTUM_CONTAINER_API_URL` is the Tutum API resource URI of the container itself.
* `TUTUM_CONTAINER_HOSTNAME` is the external hostname allocated to the container itself.

If you provide API access to your service, you can use the generated token (stored in `TUTUM_AUTH`) to access these API URLs to gather information or automate operations, such as scaling.

