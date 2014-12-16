Services can have API roles. An API role is a set of privileges granted to the service containers for the Tutum API. They will receive a token through an environment variable which can be used to query the Tutum API.

At the moment, we only support a "global" role which allows any operation to be performed on the API if granted. The API role is passed in to the service containers as an authorization token stored in an environment variable called `TUTUM_AUTH`. This variable should be use to set the `Authorization` HTTP header when calling Tutum's API:

	$ curl -H "Authorization: $TUTUM_AUTH" -H "Accept: application/json" https://dashboard.tutum.co/api/v1/application/

Using this feature, and combined with Tutum's [automatic environment variables](https://support.tutum.co/support/solutions/articles/5000012181), you can make your application inside a container read and perform operations using Tutum's API:

	$ curl -H "Authorization: $TUTUM_AUTH" -H "Accept: application/json" $WEB_TUTUM_API_URL

You can use this information for example to reconfigure a proxy container by reading the linked service list of current running containers.

Check our [API documentation](https://docs.tutum.co/v2/api/) for more information on the different API operations available.