# Introduction

Tutum supports redeployment of services while they are running. This can be used when a new version of the image is pushed to the registry and you want your service to regenerate its containers with it.

You can redeploy the latest version of the service's current image tag, or select a different tag of the same image.

When a redeployment is requested, Tutum will **terminate** the current service containers, and **deploy** new ones with the new version and/or the new image tag. Please note that:

- The new containers will be deployed according to the service tags, deployment strategies, current available nodes, port mappings, etc. They might be deployed in **different** nodes and will, in most cases, have **different** endpoints than the previous ones.
- If your containers are using volumes, the new containers will **reuse** the existing volumes, forcing the containers to be redeployed in the same nodes as the previous ones in order to satisfy this requirement.


## Redeploying a service using the web interface

Go to the detail page of the service that you would like to redeploy, and click on the **Redeploy service** button on the top right. The following modal will appear:

![](https://s.tutum.co/support/images/service-redeploy-modal.png)

Select the tag that you would like to redeploy, and click **Redeploy**. Tutum will start the redeployment inmediately.


## Redeploying a service using webhooks

You can also use webhook receivers to trigger a service redeploy. This could be useful to redeploy everytime an image is pushed or built in the Docker Hub. [Click here for more information](https://support.tutum.co/support/solutions/articles/5000513815)

# Using webhook handlers in the API and CLI

Check our [API and CLI documentation](https://docs.tutum.co/v2/api/#redeploy-a-service) for more information on how to redeploy services using our API, SDKs and the CLI.
