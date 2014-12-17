# Your first Service

## What is a service?

A services is a group of containers of the same **image:tag**. Services make it simple to scale your application. With Tutum, you simply drag a slider to increase or decrease the number of containers in a service. 

## Deploying the service

Before a service can be deployed using Tutum, you must have at least 1 node deployed. If you have not done this yet, you can learn how to deploy a node [here](https://support.tutum.co/support/solutions/articles/5000523221-your-first-node).

### Using the Web UI

Make sure the top **Services** tab is active, then click on the green button **Create your first service**

![](http://s.tutum.co.s3.amazonaws.com/support/images/create-first-service.png)

You will be taken to the wizard to launch services. The wizard has three steps, the last of which is optional:

  - **Image Selection:** to choose the container image that will be used for this service. Images can come from Tutum's Jumpstarts library, Docker's public index (i.e. Docker Hub), private registries (e.g. Tutum's private registry, quay.io, Docker's private registry).
  - **Service configuration:** to configure the service before it is created. You can choose the initial number of containers in this service, expose/publish ports, modify the run command or entrypoint, set memory and CPU limits, among other things.
  - **Environment variables:** to edit environment variables and link your service to other existing services in Tutum.

For this first service we're going to launch a simple Web service. Make sure that **Jumpstarts** is selected in the wizard, and then click on **Miscellaneous** on the far right.

![](http://s.tutum.co.s3.amazonaws.com/support/images/first-service-wizard.png)

You will see an image called `tutum/hello-world`. This image is for a container that runs Apache with a simple *hello world* webpage. 

Click on **Select** to be taken to **Step 2: Service configuration**.

In this step Tutum loads all of the available Image tags available for this image. **tutum/hello-world** only has 1 image tag called **latest**.

###Publishing a port

Since we intend to access this container over the Internet, we first need to publish a port. By default, ports are not accessible publicly. To learn more about ports click [here](https://tutum.freshdesk.com/support/solutions/articles/5000512333-port).

Click on the **Ports** table, where it says *Click to override ports defined in image*. Then click on the **Published** checkbox. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/first-service-ports.png)

We left the Node port as *dynamic*, this means that **port 80** of the container will be mapped to a random and available port in the node in which the container is deployed. If you want to force a specific port in the node, you can do so by clicking on *dynamic* and specifying a port. Please note that two containers in the same node cannot publish to the same *node port*.

Since we won't be modifying anything else in this service, we can now click on **Create and deploy** on the bottom right corner to create and deploy this service using Tutum.

![](http://s.tutum.co.s3.amazonaws.com/support/images/first-service-create-and-deploy-button.png)

Tutum will now send you to the **Timeline** inside the Service's detailed view. In the detailed view there are 7 sections/pills: 

  - **Containers**: to view a table of the containers that are part of this service and their status. This is also where a service can be scaled by launching more containers. 
  - **Links**: to see the list of services that this service is currently linked to and linked from. 
  - **Logs**: to check the recent logs from all the containers in this service.
  - **Environment variables**: to see a list of all the environment variables that are defined in this service.
  - **Monitoring**: to check the CPU, memory and bandwidth of the individual containers in this service. 
  - **Webhooks**: to add and remove redeploy webhook handlers. These webhooks can be used to automate the redeployment of a service when a new image is built or when a code update (git push) has ocurred. 
  - **Timeline**: a timeline of all the API calls, and accompanying logs, that were performed against this service.
  
In the **Timeline** you should see a log output similar to the one below. Please note that it can take a couple of minutes for the container to deploy.

```
Deploying...
Creating 1 new containers
Preparing to deploy container f93b1a05-4444-49e5-98b0-9dc3a7618453
hello-world-1: Choosing best node. Deployment strategy: BALANCE
hello-world-1: Deploying in 8468426e-tutorial.node.tutum.io
hello-world-1: Pulling image tutum/hello-world:latest in 8468426e-tutorial.node.tutum.io
hello-world-1: Creating in 8468426e-tutorial.node.tutum.io
hello-world-1: Starting with docker id df9525795bef5394e1a33b2ef42e26ba991bdccece4bc4f4f34e1def5c095fe9 in 8468426e-tutorial.node.tutum.io
hello-world-1: Inspecting and checking its configuration
hello-world-1: Running in 8468426e-tutorial.node.tutum.io
```

And this is what the interface will look like:

![](http://s.tutum.co.s3.amazonaws.com/support/images/first-service-timeline.png)

You will also notice the status, under the Service's name **hello-world**, update to **Running* once the container is deployed successfully.

Click on the **Containers** pill.

You'll see a table of all the containers (only one for now) in this service. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/first-service-container-list.png)

Clicking on the container's name takes you to the Container's detailed view (see below). In there you'll get additional information about the containers, such as endpoints, logs, monitoring, etc.

![](http://s.tutum.co.s3.amazonaws.com/support/images/first-service-container.png)

In the **Endpoints** section we see the endpoints that this container is publishing. In the screenshot above, there is a single endpoint: **hello-world-1.8468426e-borja.node.tutum.io:49153**. The endpoint is composed of both the container's hosname and a port number. 

Clicking on the link *(square and arrow icon)* to the right of the endpoint will open a new tab on your browser and display the webpage that our container is hosting.

![](http://s.tutum.co.s3.amazonaws.com/support/images/first-service-webpage.png)

**CONGRATULATIONS!!!** You have successfully deployed your first service using Tutum.

### What's next?

Learn how to scale your service [here](https://tutum.freshdesk.com/support/solutions/articles/5000012179-service-scaling).

