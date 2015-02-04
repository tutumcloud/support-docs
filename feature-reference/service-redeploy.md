# Introduction

Tutum supports redeployment of services while they are running. This can be used when a new version of the image is pushed to the registry and you want your service to regenerate its containers with it, or if you have modified any attributes of the service and you want to apply them.

When a redeployment is requested, Tutum will **terminate** the current service containers, and **deploy** new ones using the latest service definition. Please note that:

- The new containers will be deployed according to the service tags, deployment strategies, current available nodes, port mappings, etc. They might be deployed in **different** nodes.
- Container **hostnames** will remain the same (`servicename-1.username.cont.tutum.io`), but if your service uses dynamic ports, new ones will be used when you redeploy.
- If your containers are using volumes, the new containers will **reuse** the existing volumes, forcing the containers to be redeployed in the same nodes as the previous ones in order to satisfy this requirement. If you changed your service or node tags, and a node where a volume is stored does not match the new tags, the redeploy will fail.


## Current limitations

- If you have another service which is linked to the one you are redeploying, the **link** will be broken and you will have to redeploy it as well. This is will change in the future.


## Redeploying a service using the web interface

Go to the detail page of the service that you would like to redeploy, and click on the **Redeploy** button on the top right. The following confirmation modal will appear:

![](https://s.tutum.co/support/images/redeploy-service.png)

Click **OK** and Tutum will start the redeployment inmediately.


## Redeploying a service using webhooks

You can also use webhook receivers to trigger a service redeploy. This could be useful to redeploy everytime an image is pushed or built in the Docker Hub. [Click here for more information](https://support.tutum.co/support/solutions/articles/5000513815)

# Using webhook handlers in the API and CLI

Check our [API and CLI documentation](https://docs.tutum.co/v2/api/#redeploy-a-service) for more information on how to redeploy services using our API, SDKs and the CLI.
