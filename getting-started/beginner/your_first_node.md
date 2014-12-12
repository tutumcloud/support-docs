# Your first Node

## What is a node?

A node is an individual Linux host used to deploy and run your applications. Tutum does not provide any hosting services, which means all of your applications, services, containers, etc. run on your own hosts. These hosts can come from different sources, such as physical servers, virtual machines or cloud providers. 

Tutum makes it easy to provision nodes from your existing cloud providers. If you already have an account with an infrastructure as a service provider, you can provision new nodes directly from within Tutum. Today there is native support for Amazon Web Services, Digital Ocean and Microsoft Azure. 

Tutum also supports users bringing their own node. This is the ability to use any existing Linux host connected to the Internet as a Tutum node. The way this works is by simply installing an agent. This agent registers itself with your account, allowing you to deploy your containerized applications using Tutum.

## Your first node

### Using a Public IaaS Cloud Provider

You can provision nodes directly from within Tutum (using the Web UI, CLI or API) provided that you grant Tutum access to your IaaS Cloud Provider. This can be done by linking your account from Amazon Web Services (using [IAM](https://console.aws.amazon.com/iam) and an Access Key ID  + Secret Access Key), or Digital Ocean (using OAuth), or Microsoft Azure (using OAuth). 

To link your Cloud Provider accounts, click on your username on the topi right corner of the application > **Account info** > **Cloud providers**. Or click [here](https://dashboard.tutum.co/account/).

There are  detailed tutorials on how to link your account for each of the supported providers:

  - [Amazon Web Services](https://support.tutum.co/support/solutions/articles/5000224910-link-your-amazon-web-services-account-to-tutum)
  - [Digital Ocean](https://support.tutum.co/support/solutions/articles/5000012151-link-your-digital-ocean-account-to-tutum)
  - [Microsoft Azure]()
  
When launching a node from a cloud provider you'll actually be creating node clusters. Node Clusters are logical groups of nodes of the same type and from the same cloud provider. Node clusters allow you to scale the infrastructure by provisioning more nodes with a drag of a slider.
  
  
### Using "Bring your own node"

Alternatively, if you do not wish to use your existing account at one of the supported cloud providers, or if you do not have an account, you can turn any Linux host that is connected to the Internet into a full-fledge Tutum node. 

Find all the information on how to turn a Linux node into a node by installing the Tutum agent [here](https://support.tutum.co/support/solutions/articles/5000513678-bring-your-own-node).

### What's next?

Now that you've got at least one node deployed, it's time to deploy your first service. Remember that a service is a group of containers from the same container image. Services make it simple to scale your application across a number of nodes. Services can also be linked one to another even if they are deployed on different nodes, regions, or even cloud providers. 

Click [here](https://support.tutum.co/support/solutions/articles/5000012154-deploy-your-first-service) to continue reading the tutorial on how to deploy your first service.





