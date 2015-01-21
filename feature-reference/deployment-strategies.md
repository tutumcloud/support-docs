Tutum can use different scheduling algorithms when deploying containers to more than one node. At the moment, the following deployment strategies are available:


## Available strategies

### Balance

This is the default strategy. A service with a `BALANCE` strategy, will deploy its containers to the node with the **lower number of running containers** at the time of the deployment.


### Every node

A service with an `EVERY NODE` strategy will have one container deployed **on each node**. With every new node, a new container will be deployed to it. It has the following properties:

* It cannot be scaled, as the target number of containers will always be the number of deployed nodes.
* If the service uses volumes, each container on each node will have a different volume.
* If the service is linked from another service with `EVERY NODE` strategy, containers will be linked one-to-one on each node.



## Planned strategies

Interested to see a new deployment strategy implemented? [Please tell us!](https://support.tutum.co/support/discussions/forums/5000044393)