# Introduction

**Deployment tags** are used to target the deployment of services to a specific set of nodes. You can specify one or more tags to nodes and services. Tags specified to node clusters are automatically assigned to nodes within that cluster. Services with tags will be deployed to nodes that match **all** tags assigned to that service.

For example, if we have the following nodes:

Node name | Tags
--------- | ---- 
my-node-dev | `aws` `us-east-1` `development` `test` `frontend` `backend`
my-node-prod-1 | `aws` `us-east-1` `production` `frontend`
my-node-prod-2 | `aws` `us-east-2` `production` `frontend`
my-node-prod-3 | `aws` `us-east-1` `production` `backend`
my-node-prod-4 | `aws` `us-east-2` `production` `backend`

And we deploy the following service:

Service name | Tags
------------ | ---- 
my-webapp-dev | `development` `frontend`

All containers for service `my-webapp-dev` will be deployed to node `my-node-dev` as it contains both `development` *and* `frontend` tags.

If we were to deploy the following production service:

Service name | Tags
------------ | ---- 
my-webapp-prod | `production` `frontend`

All containers for service `my-webapp-prod` will be deployed to nodes `my-node-prod-1` and `my-node-prod-2` as they both contain `production` *and* `frontend` tags. Distribution between those nodes will be done depending on the deployment algorithm used (at the moment, the only deployment algorithm available is the *BALANCE* algorithm that will deploy each container to the node with the least number of containers running).


## Automatic deployment tags

When you launch a node cluster, three tags are assigned automatically to the node cluster and all nodes within that cluster:

* Provider name (e.g. `digitalocean`, `aws`)
* Region name (e.g. `us-east-1`, `lon1`)
* Node cluster name (e.g. `my-node-cluster-dev-1`)


# Using deployment tags in the web UI

## Assigning tags to nodes

Go to the **Launch new node cluster** wizard:

![](https://s.tutum.co/support/images/nodecluster-wizard-tags.png)

In the **Deploy tags** field, enter the tags that you want to assign to this cluster and all nodes within it. When the node cluster scales up, new nodes will automatically inherit the tags of the node cluster. Note that the tags described in section *Automatic deployment tags* above will be assigned after the node cluster is created automatically.

Once it's deployed, you can see the tags that have been assigned to that node cluster on the left side:

![](https://s.tutum.co/support/images/nodecluster-detail-tags.png)

To change them, click on the tags and an editable field will appear. Add and remove tags as desired, and click **Save**. Tags will be added and/or removed in all child nodes.

You can also add tags to individual nodes which are different from the node cluster ones. To do that, click on a node to go to the node detail view:

![](https://s.tutum.co/support/images/node-detail-tags.png)

Click on the tags on the left side and an editable field will appear. Add and remove tags as desired, and click **Save**. Tags will be added and/or removed in this node only.


## Assigning tags to services

In order to target deployments using tags, you have to specify one or more tags to your services. If you don't provide any tags to a service, it will be deployed to all available nodes.

Go to the **Create new service** wizard:

![](https://s.tutum.co/support/images/service-wizard-tags.png)

In the **Deploy tags** field, enter the tags that you want to assign to this service. Tags in a service define which nodes will be used on deployment: only nodes that match *all* tags specified in the service will be used for deployment.

After the service is deployed, tags can also be added and removed. Go to the service detail view:

![](https://s.tutum.co/support/images/service-detail-tags.png)

In order to deploy containers to the nodes filtered by the new set of tags, terminate all containers (or scale down to zero) and scale back up. New containers will be deployed to the nodes that match the new tags.


# Using deployment tags in the API and CLI

Check our [API and CLI documentation](https://docs.tutum.co/v2/api/#tags) for more information on how to use tags with our API, SDKs and the CLI.
