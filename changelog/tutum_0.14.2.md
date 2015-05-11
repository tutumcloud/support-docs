# Tutum 0.14.2

## Added 

- **Introducing the 'Deploy to Tutum' button**. You can now add a _Deploy to Tutum_ button on your GitHub repositories to let other Tutum users deploy your stack files in just one click. [Learn more](https://support.tutum.co/support/solutions/articles/5000620449)

  ![Deploy to Tutum Button](http://s.tutum.co.s3.amazonaws.com/changelog/0.14.2/Deploy-to-tutum-Github.png)

- **New 'Scale Up' trigger**. You're now able to create a trigger on a service that, when called, will scale the service by one container. This is especially useful for administrative tasks. [Learn more](https://support.tutum.co/support/solutions/articles/5000513815)
- **Added last monitoring metric to REST API**. We have added a `last_metric` attribute to containers and nodes to our REST API which contain the last CPU, memory and disk space monitoring metric received. [Learn more](https://docs.tutum.co/v2/api/?shell#containers)

## Changed

- **Webhook Handlers are now called 'Triggers'**. Existing trigger URLs will continue to work, but new triggers will get an updated URL.
- **Environment variables can contain Tutum-specific variables**. We now expand user-defined environment variables which contain Tutum-specific variables, such as `$TUTUM_NODE_FQDN`. You can reference these in your services and they will be evaluated per container at deploy time.
- **Action URIs are now returned in our REST API**. We now add a header `X-Tutum-Action-URI` which holds the resource URI of the action that was created because of the HTTP request. This can be used to know the outcome of an asynchronous operation, such as a service redeploy or a node cluster scale.
- **Reduced footprint of our system containers**. We have switched our system container images to use [alpine](https://registry.hub.docker.com/_/alpine/) and made a few improvements to reduce their storage footprint on the nodes.

## Fixed

- **Azure integration now uses certificates**, solving the previous known issue where OAuth tokens expired after a short period of time. [Learn more](https://support.tutum.co/support/solutions/articles/5000560928-link-your-microsoft-azure-account)
- **Redeploy triggers now send a callback to DockerHub** when the operation has finished.
- **Stabilized container and node monitoring information**. We have also reduced the number of available time periods for monitoring to just the last 24 hours.
- **Fixed a bug on container redeploy**, which caused the new container to ignore the deployment strategy set in the service.
- We now allow empty values on environment variables and square brackets `[]` on environment variable keys
- Other bug fixes and stability improvements


