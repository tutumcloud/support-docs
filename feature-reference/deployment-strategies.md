Tutum can use different scheduling algorithms when deploying containers to more than one node. At the moment, the following deployment strategies are available:


## Available strategies

### Emptiest node

This is the default strategy. A service with a `EMPTIEST_NODE` strategy will deploy its containers to the nodes that match its deploy tags with the **lowest total number of containers** at the time of each container's deployment, regardless of the service. This strategy tipically balances the total load of all services across all nodes.


### High availability

A service with a `HIGH_AVAILABILITY` strategy will deploy its containers to the node that matches its deploy tags with the **lowest number of containers of that service** at the time of each container's deployment. This means that the containers will be spread across all nodes that match the deploy tags for the service. This is tipically used to increase the service availability


### Every node

A service with an `EVERY_NODE` strategy will have one container deployed **on each node** that matches its deploy tags. It has the following properties:

* With every new node that matches the service's deploy tags, a new container will be deployed to it. 
* It cannot be manually scaled.
* If the service uses volumes, each container on each node will have a different volume.
* If the service is linked from another service with `EVERY_NODE` strategy, containers will be linked one-to-one on each node.


## Planned strategies

Interested to see a new deployment strategy implemented? [Please tell us!](https://support.tutum.co/support/discussions/forums/5000044393)