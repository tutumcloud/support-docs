# Tutum 0.14.0

## Added 

- **New Stream API** announced, starting with an endpoint to stream [Tutum Events](https://docs.tutum.co/v2/api/?python#tutum-event). Support in the [Tutum Python SDK](https://docs.tutum.co/v2/api/?python#listen-to-new-tutum-events) has been added. [Learn more](http://blog.tutum.co/2015/04/07/presenting-tutum-stream-api/)

- **Service discovery using names as hostnames** to allow containers to resolve any other container or service in the same or different stack without the need for links. [Learn more](https://support.tutum.co/support/solutions/articles/5000012181-service-discovery-and-links)

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/service_discovery.png)

- **Environment variables are now expanded** using the local shell environment when creating or updating a stack using the Tutum CLI. This means you can use the environment variables locally defined in your shell to define those in the stack. [Learn more](https://support.tutum.co/support/solutions/articles/5000583471-stack-yaml-reference).


## Changed

- **Service Redeploy triggers are now queued** when there is an action being performed on the service or any of its containers.
- **Tags nested API endpoint has been removed**. To add or remove tags on any object, use the `PATCH` operation to update its `tags` attribute instead. [Learn more](https://docs.tutum.co/v2/api/#update-an-existing-service)


## Fixed

- **Error notifications now only show once**. We fixed a bug where error notifications reappeared on the web UI when changing screens.
- **Fixed environment variables for links in service detail view**. In certain circumstances, the keys of the environment variables created from links were incorrectly shown in the service detail view.
