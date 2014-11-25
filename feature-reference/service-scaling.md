If the service that you are deploying supports horizontal scaling, Tutum makes it easy to spawn new instances (containers) with your service to handle any additional load.

## **What can be scaled horizontally?[](https://docs.tutum.co/features/scaling/#what-can-be-scaled-horizontally "Permalink to this headline")** 

Any service that can handle additional load by just increasing the
number of instances (containers) of such service. Examples include:

-   Stateless web servers and proxies that listen in port 80
-   “Worker” instances that process jobs from a queue and do not receive
    user traffic
-   “Cron”-style instances that execute periodic tasks and do not
    receive user traffic

Usually, databases cannot be scaled horizontally by just increasing the
number of instances. The application has to be configured specifically
to handle horizontal scaling, for example, for MySQL to automatically
configure itself as a master or a slave instance depending on the number
of existing instances in the cluster. A custom proxy is usually deployed
in these scenarios to route traffic to the appropriate instance.

##**Deployment and scaling modes[](https://docs.tutum.co/features/scaling/#deployment-and-scaling-modes "Permalink to this headline")**

There are two modes of deployment of multiple containers for a service:

-   **Parallel mode**: all the containers of the service will be
    deployed at the same time without any links between them. This is
    the fastest way of deployment and is the default.
-   **Sequential mode**: each new container deployed for the service
    will be linked to all previous containers, making complex scaling
    setups possible within the containers bootstrap logic. This mode is
    explained in detail in the following sections.

### **Using the API[](https://docs.tutum.co/features/scaling/#using-the-api "Permalink to this headline")** 

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

### **Using the CLI[](https://docs.tutum.co/features/scaling/#using-the-cli "Permalink to this headline")** 

You can set the `sequential_deployment` option when deploying an
application through the CLI: 

``` 
$ tutum service run --sequential_deployment [...] 
```
### **Using the web interface**

You can activate the **Sequential deployment** setting on the **Service
configuration** step of the **Launch new service** wizard:

![](http://s.tutum.co.s3.amazonaws.com/support/images/service-wizard-sequential-deployment.png)

## **How Tutum handles sequential deployment and scaling[](https://docs.tutum.co/features/scaling/#how-tutum-handles-sequential-deployment-and-scaling "Permalink to this headline")**

When a service is launched with more than one container, the second and
subsequent containers are linked to all the previous ones. These
environment variables are very useful if your service needs to
autoconfigure itself when launching and depends on the number of
instances already running. For example, if a service
named `my-web-app` is launched with **3 **containers, each instance will
be started with the following environment variables:

### **Environment variables set in the first (my-web-app-1) container[](https://docs.tutum.co/features/scaling/#environment-variables-set-in-the-first-my-web-app-1-container "Permalink to this headline")** 

The first container will not have any special environment variables set
by the scaling mechanism

### **Environment variables set in the second (my-web-app-2) container[](https://docs.tutum.co/features/scaling/#environment-variables-set-in-the-second-my-web-app-2-container "Permalink to this headline")**

The second container will be linked to the first container
(`my-web-app-1`), ending up with the following environment variables:

Name | Value
--- | --- 
MY\_WEB\_APP\_1\_PORT | [tcp://my-web-app-1-user.beta.tutum.io:49330](tcp://my-web-app-1-user.beta.tutum.io:49330)
MY\_WEB\_APP\_1\_PORT\_80\_TCP | [tcp://my-web-app-1-user.beta.tutum.io:49330](tcp://my-web-app-1-user.beta.tutum.io:49330)
MY\_WEB\_APP\_1\_PORT\_80\_TCP\_ADDR  |  my-web-app-1-user.beta.tutum.io
MY\_WEB\_APP\_1\_PORT\_80\_TCP\_PORT  |  49330
MY\_WEB\_APP\_1\_PORT\_80\_TCP\_PROTO |  tcp

### **Environment variables set in the third (my-web-app-3) container[](https://docs.tutum.co/features/scaling/#environment-variables-set-in-the-third-my-web-app-3-container "Permalink to this headline")** 

The third container will be linked to the first and second containers
(`my-web-app-1` and `my-web-app-2`), ending up with the following
environment variables:

Name | Value
--- | --- 
  MY\_WEB\_APP\_1\_PORT      |             [tcp://my-web-app-1-user.beta.tutum.io:49330](tcp://my-web-app-1-user.beta.tutum.io:49330)
  MY\_WEB\_APP\_1\_PORT\_80\_TCP     |     [tcp://my-web-app-1-user.beta.tutum.io:49330](tcp://my-web-app-1-user.beta.tutum.io:49330)
  MY\_WEB\_APP\_1\_PORT\_80\_TCP\_ADDR  |  my-web-app-1-user.beta.tutum.io
  MY\_WEB\_APP\_1\_PORT\_80\_TCP\_PORT  |  49330
  MY\_WEB\_APP\_1\_PORT\_80\_TCP\_PROTO |  tcp
  MY\_WEB\_APP\_2\_PORT             |      [tcp://my-web-app-2-user.delta.tutum.io:49331](tcp://my-web-app-2-user.delta.tutum.io:49331)
  MY\_WEB\_APP\_2\_PORT\_80\_TCP   |       [tcp://my-web-app-2-user.delta.tutum.io:49331](tcp://my-web-app-2-user.delta.tutum.io:49331)
  MY\_WEB\_APP\_2\_PORT\_80\_TCP\_ADDR  |  my-web-app-2-user.delta.tutum.io
  MY\_WEB\_APP\_2\_PORT\_80\_TCP\_PORT  |  49331
  MY\_WEB\_APP\_2\_PORT\_80\_TCP\_PROTO |  tcp

## **Setting the initial number of containers[](https://docs.tutum.co/features/scaling/#setting-the-initial-number-of-containers "Permalink to this headline")** 

When configuring your service prior to launch, you will have the chance
to specify an initial number of containers for your application:

![](http://s.tutum.co.s3.amazonaws.com/support/images/service-wizard-scale.png)

The number of containers specified in this wizard will be launched
immediately.

##**Scaling an already running service[](https://docs.tutum.co/features/scaling/#scaling-an-already-running-application "Permalink to this headline")** 

After your service has been started, if you need to scale it up (or
down), you can do so from the service detail page:

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001219299/original/Service_pre-scale.png?1411926402)


Simply move the **Number of containers** slider to the target number of
containers and press **Apply**. The application will start scaling
immediately.

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001219315/original/Service_scaling.png?1411926427)

