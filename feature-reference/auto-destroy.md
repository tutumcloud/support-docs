**Autodestroy** is a Tutum feature that when enabled on a service, will automatically terminate containers when they stop (destroying all data within the container). This is useful for one-off actions which store results in a external system. It can be set with the following values:

-   `OFF`: if the container stops, regardless of the exit code, Tutum
    will not terminate it and will it in **Stopped** state.
-   `ON_FAILURE`: if the container stops with an exit code different
    from 0, Tutum will automatically terminate it. Otherwise, it will
    leave it in **Stopped** state.
-   `ALWAYS`: if the container stops, regardless of the exit code,
    Tutum will automatically terminate it.

If **Autorestart** is activated, Tutum will evaluate whether to try restarting the container or not before evaluating **Autodestroy**.

## Launching a Service with Autodestroy

### Using the API 

You can enable autodestroy when launching a service through the API:

```
POST /api/v1/service/ HTTP/1.1 
{
	 "autodestroy": "ALWAYS", 
	 [...] 
} 
```

If not provided, it will have a default value of `OFF`. Check our [API documentation](https://docs.tutum.co/v2/api/?http) for more information.

### Using the CLI

You can enable autodestroy when launching a service using the CLI:

```
$ tutum service run --autodestroy ALWAYS [...] 
```

If not provided, it will have a default value of `OFF`. Check our [API documentation](https://docs.tutum.co/v2/api/?shell) for more information.


### Using the web interface

At the moment, activating the **Autodestroy** setting on
the **Service configuration** step of the **Launch new
service** wizard sets the autodestroy setting to `ALWAYS`.

![](https://s.tutum.co/support/images/service-wizard-autodestroy.gif)

The default value is to be *deactivated* which will set it to `OFF`.

## Activating Autodestroy to an already deployed service

### Using the API

You can set the autodestroy option after the service has been
deployed through the API:

```
PATCH /api/v1/service/(uuid)/ HTTP/1.1 
{ 
	"autodestroy": "ALWAYS" 
} 
```

Check our [API documentation](https://docs.tutum.co/v2/api/?http) for more information.


### Using the CLI

You can set the autodestroy option after the service has been
deployed using the CLI:

```
$ tutum apps set --autodestroy ALWAYS (name or uuid) 
```

Check our [API documentation](https://docs.tutum.co/v2/api/?shell) for more information.


### Using the web interface

You can also activate or deactivate the autodestroy setting to a service
after it has been deployed from within the service detail page.

![](https://s.tutum.co/support/images/service-autodestroy-enable-disable.gif)

You can click on the **Autodestroy** button to set the feature to `ALWAYS` (ON) or `OFF`.