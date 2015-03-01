Tutum supports redeployment of services while they are running. This can be used when a new version of the image is pushed to the registry and you want your service to regenerate its containers with it, or if you have modified any attributes of the service and you want to apply them.

When a redeployment is requested, Tutum will **terminate** the current service containers, and **deploy** new ones using the latest service definition. Please note that:

- The new containers will be deployed according to the service tags, deployment strategies, current available nodes, port mappings, etc. They might be deployed in **different** nodes.
- Container **hostnames** will remain the same (`servicename-1.username.cont.tutum.io`), but if your service uses **dynamic published ports**, new ones might be used when you redeploy.
- If your containers are using volumes, the new containers will **reuse** the existing volumes, forcing the containers to be redeployed in the same nodes as the previous ones in order to satisfy this requirement. If you changed your service or node tags, and a node where a volume is stored does not match the new tags, the redeploy will fail.
- When redeploying a service, containers will keep their local IPs even if they end up in different nodes after the redeployment. This means that linked services don't need to be redeployed.


## Redeploying a service using the web interface

Go to the detail page of the service that you would like to redeploy, and click on the **Redeploy** button on the top right. The following confirmation modal will appear:

![](https://s.tutum.co/support/images/redeploy-service.png)

Click **OK** and Tutum will start the redeployment immediately.

## Redeploying a service using the API and CLI

Check our [API and CLI documentation](https://docs.tutum.co/v2/api/#redeploy-a-service) for more information on how to redeploy services using our API, SDKs and the CLI.


## Redeploying a service using webhooks

You can also use **webhook receivers** to trigger a service redeploy. This could be useful to redeploy a service everytime its image is pushed or rebuilt in the Docker Hub. [Click here for more information](https://support.tutum.co/support/solutions/articles/5000513815)

## Autoredeploy on image push to Tutum Registry

If your service uses a private image stored in Tutum's Registry, you can use the **Autoredeploy** feature on the service to trigger automatic redeployments whenever an image is pushed without the need to use a webhook handler. [Click here for more information](https://support.tutum.co/support/solutions/articles/5000569896)