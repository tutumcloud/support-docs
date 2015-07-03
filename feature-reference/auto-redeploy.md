**Autoredeploy** is a Tutum feature that when enabled on a service that uses an image stored in Tutum's Registry, will automatically redeploy it whenever a new image is pushed or built.

**Note:** if you want to autoredeploy your image stored in the Docker Hub or another third party registry, you will need to use [redeploy triggers](https://support.tutum.co/support/solutions/articles/5000513815) instead.


## Launching a service with autoredeploy

### Using the web interface

You can enable **autoredeploy** setting on the **Service configuration** step of the **Launch new service** wizard.

![](https://s.tutum.co/support/images/service-wizard-autoredeploy.png)

The default value is to be *deactivated*.


### Using the CLI

You can enable **autoredeploy** when launching a service using the CLI:

```
$ tutum service run --autoredeploy [...] 
```

If not provided, it will have a default value of `false`. Check our [API documentation](https://docs.tutum.co/v2/api/?shell) for more information.


### Using the API 

You can enable **autoredeploy** when launching a service through the API:

```
POST /api/v1/service/ HTTP/1.1 
{
	 "autoredeploy": true, 
	 [...] 
} 
```

If not provided, it will have a default value of `false`. Check our [API documentation](https://docs.tutum.co/v2/api/?http) for more information.


## Activating autoredeploy to an already deployed service

### Using the web interface

You can also activate or deactivate the **autoredeploy** setting of a service after it has been deployed from within the service detail page. Click on the **Edit** buton, change the **autoredeploy** setting on the form, and click **Save**.


### Using the CLI

You can set the **autoredeploy** option after the service has been deployed using the CLI:

```
$ tutum service set --autoredeploy (name or uuid) 
```

Check our [API documentation](https://docs.tutum.co/v2/api/?shell) for more information.


### Using the API

You can set the **autoredeploy** option after the service has been deployed through the API:

```
PATCH /api/v1/service/(uuid)/ HTTP/1.1 
{ 
	"autoredeploy": true
} 
```

Check our [API documentation](https://docs.tutum.co/v2/api/?http) for more information.
