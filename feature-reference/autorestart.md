**Autorestart** is a service-level setting that will automatically start your containers whenever they stop or crash. It has the following options:

- `OFF`: if the container stops, regardless of the exit code, it won't be autorestarted and will stay in **Stopped** state.
- `ON_FAILURE`: if the container stops with an exit code different from 0, it will be autorestarted.
- `ALWAYS`: if the container stops, regardless of the exit code, it will be autorestarted.

Please note that **Autorestart** is incompatible with **Autodestroy** in the following scenario:

- If **Autorestart** is set to `ALWAYS`, **Autodestroy** has to be `OFF`

The **Autorestart** feature is implemented using Docker's `--autorestart` flag, so Docker will try to restart the container indefinitely until it succeeds using an incremental back-off algorithm.

If the Docker daemon in the node is restarted (because it has been upgraded, or because the underlying node has been restarted), only containers launched within a service with **Autorestart** set to `ALWAYS` will be started automatically.


## Launching a Service with Autorestart 

### Using the API

You can specify the **Autorestart** option when launching
a service through the API:

```
POST /api/v1/service/ HTTP/1.1 
{ 
	"autorestart": "ON_FAILURE",
	[...] 
} 
```

If not provided, it will have a default value of `OFF`. Check our [API documentation](https://docs.tutum.co/v2/api/?http) for more information.

### Using the CLI

You can specify the **Autorestart** option when launching a service using the CLI:

```
$ tutum service run --autorestart ON_FAILURE [...] 
```

If not provided, it will have a default value of `OFF`. Check our [API documentation](https://docs.tutum.co/v2/api/?shell) for more information.

### Using the web interface

At the moment, activating the **Autorestart** setting on the **Service configuration** step of the **Launch new service ** wizard sets the **autorestart** settings to `ALWAYS`.

![](https://s.tutum.co/support/images/autorestart.gif)

The default value is to be *deactivated* which will set the option to `OFF`.


## Activating Crash Recovery to an already deployed service 

### Using the API
 
You can set the **Autorestart** option after the service has been deployed through the API:

```
PATCH /api/v1/service/(uuid)/ HTTP/1.1 
{ 
	"autorestart": "ALWAYS",
} 
```

Check our [API documentation](https://docs.tutum.co/v2/api/?http) for more information.

### Using the CLI

You can set the **Autorestart** option after the application has been deployed using the CLI:

``` 
$ tutum service set --autorestart ALWAYS (name or uuid) 
```

Check our [API documentation](https://docs.tutum.co/v2/api/?shell) for more information.

### Using the web interface

You can also activate or deactivate **Autorestart** to a service after it has been deployed editing the service.
