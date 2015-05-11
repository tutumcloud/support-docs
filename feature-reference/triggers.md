**Triggers** are API endpoints that will redeploy or scale a certain service whenever a `POST` HTTP request is sent to them. You can create one or more triggers per service. They don't require any authorization to be called, so third party services like Docker Hub can call them. Because of this, is very important to keep their URLs secret.

The body of the `POST` request will be passed into the new containers as an environment variable `TUTUM_TRIGGER_BODY`.


## Creating triggers

We support two types of triggers:

* **Redeploy** triggers, which will redeploy the service when called
* **Scale up** triggers, which will scale the service by one or more containers when called

Go to the detail page of the service that you would like to create a new trigger to, and click on the **Triggers** tab:

![](https://s.tutum.co/support/images/triggers-tab-blank.png)

In the **Add trigger** field, enter a name for the trigger, select a trigger type, and click **Add**. The following modal window will appear:

![](https://s.tutum.co/support/images/new-trigger-created.png)

Copy the URL provided and use it in your application or third party service webhook configuration.


## Using redeploy triggers with the Docker Hub

If you use the [Docker Hub](https://registry.hub.docker.com/) to store your repositories, you can set up a webhook in your repository settings to automatically redeploy your service whenever a new version of the repository is pushed or built if you are using trusted builds.

For this, go to your repository settings and click on **Webhooks**:

![](https://s.tutum.co/support/images/dockerhub-image-detail-webhooks.png)

In the **Webhooks** screen, click on **Add Webhook**, give the webhook a **Short name** and paste the trigger URL you created earlier in the **URL 1** field, and click **Save**:

![](https://s.tutum.co/support/images/add-webhook-dockerhub.png)

Once it's added, any push to the repository will automatically trigger a redeploy of the service in Tutum.


## Revoking triggers

If you want to revoke a trigger so it stops working, go to the detail page of the service and click on the **Triggers** tab. Then, click on the **Revoke** button on the trigger you would like to revoke:

![](https://s.tutum.co/support/images/revoke-trigger.png)

After the trigger is revoked, it will stop accepting requests.


## Using triggers in the API and CLI

Check our [API and CLI documentation](https://docs.tutum.co/v2/api/#triggers) for more information on how to use triggers with our API, SDKs and the CLI.
