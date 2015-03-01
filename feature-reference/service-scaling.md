If the service that you are deploying supports horizontal scaling, Tutum makes it easy to spawn new containers of your service to handle additional load.

## What can be scaled horizontally?

Any service that can handle additional load by just increasing the
number of containers of such service. Examples include:

-   Stateless web servers and proxies
-   “Worker” instances that process jobs from a queue
-   “Cron”-style instances that execute periodic tasks

Usually, databases cannot be scaled horizontally by just increasing the number of instances. The application has to be configured specifically to handle horizontal scaling, for example, for MySQL to automatically configure itself as a master or slave depending on the number of existing instances in the service. A custom proxy is usually deployed in these scenarios to route traffic to the appropriate instance, or the client application is configured appropiately.

## Deployment and scaling modes

There are two modes of deployment of multiple containers for a service:

-   **Parallel mode**: all containers of a service will be
    deployed at the same time without any links between them. This is
    the fastest way of deployment and is the default.
-   **Sequential mode**: each new container deployed for the service
    will be linked to all previous containers, making complex scaling
    setups possible within the containers bootstrap logic. This mode is
    explained in detail in the following sections.

### Using the API

You can set the `sequential_deployment` option when deploying an
application through the API:

```
POST /api/v1/service/ HTTP/1.1 
{
	"sequential_deployment": true, 
	[...]
} 
```

See [create a new service](https://docs.tutum.co/v2/api/#service) for
more information.

### Using the CLI

You can set the `sequential_deployment` option when deploying an
application through the CLI: 

``` 
$ tutum service run --sequential [...] 
```

### Using the web interface

You can activate the **Sequential deployment** setting on the **Service
configuration** step of the **Launch new service** wizard:

![](https://s.tutum.co/support/images/service-wizard-sequential-deployment.png)


## How Tutum handles sequential deployment and scaling

When a service is deployed with more than one container and has **sequential deployment** activated, the second and subsequent containers are linked to all the previous ones. These links are very useful if your service needs to autoconfigure itself on boot depending on the number of instances already running in the service.

Check the [Service links](/support/solutions/articles/5000012181) article for a list of environment variables and hostnames that the links will create in your containers.


## Setting the initial number of containers

### Using the web interface

When configuring your service prior to launch, you will have the chance to specify an initial number of containers for your service:

![](https://s.tutum.co/support/images/service-wizard-scale.png)

The number of containers specified in this wizard will be launched immediately.

### Using the API

You can specify the initial number of containers for a service when deploying it through the API:

```
POST /api/v1/service/ HTTP/1.1 
{
	 "target_num_containers": 2, 
	 [...] 
} 
```

If not provided, it will have a default value of `1`. Check our [API documentation](https://docs.tutum.co/v2/api/?http) for more information.


### Using the CLI

You can specify the initial number of containers for a service when deploying it using the CLI:

```
$ tutum service run -t 2 [...]
```

If not provided, it will have a default value of `1`. Check our [CLI documentation](https://docs.tutum.co/v2/api/?shell) for more information.


## Scaling an already running service

### Using the web interface

After your service has been started, if you need to scale it up (or down), you can do so from the service detail page:

![](https://s.tutum.co/support/images/service-before-scaling.png)

Simply move the **Number of containers** slider to the target number of containers and press **Apply**. The application will start scaling immediately.

![](https://s.tutum.co/support/images/service-during-scaling.png)


### Using the API

You can scale an already running service through the API:

```
PATCH /api/v1/service/(uuid)/ HTTP/1.1 
{
	 "target_num_containers": 2
} 
```

### Using the CLI

You can scale an already running service using the CLI:

```
$ tutum service scake (uuid or name) 2
```

