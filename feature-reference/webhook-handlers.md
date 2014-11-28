# Introduction

**Webhook Handlers** are API endpoints that will redeploy a certain service whenever a `POST` HTTP request is sent to them. You can create one or more webhook handlers per service. They don't require any authorization to be called, so third party services like Docker Hub can call them. Because of this, is very important to keep their URLs secret.


## Creating webhook handlers

Go to the detail page of the service that you would like to create a new webhook handler to, and click on the **Webhooks** tab:

![](https://s.tutum.co/support/images/service-detail-webhooks.png)

In the **Add webhook** field, enter a name for the webhook handler, and click **Add**. The following modal window will appear:

![](https://s.tutum.co/support/images/webhook-add.png)

Copy the URL provided and use it in your application or third party service webhook configuration.


## Using a webhook handler with Docker Hub

If you use the [Docker Hub](https://registry.hub.docker.com/) to store your repositories, you can set up a webhook handler in your repository settings to automatically redeploy your service whenever a new version of the repository is pushed or built if you are using trusted builds.

For this, go to your repository settings and click on **Webhooks**:

![](https://s.tutum.co/support/images/dockerhub-image-detail-webhooks.png)

In the **Webhooks** screen, paste the webhook handler URL you created earlier in the **Hook URL** field, and click **add**:

![](https://s.tutum.co/support/images/dockerhub-webhooks.png)

Once it's added, any push to the repository will automatically trigger a redeploy of the service in Tutum.


## Revoking webhook handlers

If you want to revoke a webhook handler so it stops working, go to the detail page of the service and click on the **Webhooks** tab. Then, click on the **Revoke** button on the webhook handlers you would like to revoke:

![](https://s.tutum.co/support/images/service-detail-webhooks-revoke.png)

After the webhook handler is revoked, it will stop accepting requests.


# Using webhook handlers in the API and CLI

Check our [API and CLI documentation](https://docs.tutum.co/v2/api/#webhooks) for more information on how to use webhook handlers with our API, SDKs and the CLI.
