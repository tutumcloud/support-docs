**Autodestroy** is a Tutum feature that when enabled on an service, will automatically terminate containers when they stop (destroying all data within the container). This is useful for one-off actions which store results in a external system. It can be set with the following values:

-   **OFF**: if the container stops, regardless of the exit code, Tutum
    will not terminate it and will it in **Stopped** state.
-   **ON\_FAILURE**: if the container stops with an exit code different
    from 0, Tutum will automatically terminate it. Otherwise, it will
    leave it in **Stopped** state.
-   **ALWAYS**: if the container stops, regardless of the exit code,
    Tutum will automatically terminate it.

If **Autorestart** and/or **Autoreplace** are activated, Tutum will try
to perform those actions before **Autodestroy**.

## Launching a Service with Autodestroy
###**Using the API[](https://docs.tutum.co/features/autodestroy/#launching-an-application-with-autodestroy-activated-through-the-api "Permalink to this headline")** 

You can enable autodestroy when launching an service through the
API:

``` 
{
	 "autodestroy": "ALWAYS", 
	 [...] 
} 
```

If not provided, it will have a default value of **OFF**. See [*Create a
new cluster*](https://docs.tutum.co/v2/api/?http#create-a-new-node-cluster) for
more information.

###**Using the CLI[](https://docs.tutum.co/features/autodestroy/#launching-an-application-with-autodestroy-activated-through-the-cli "Permalink to this headline")** 

You can enable autodestroy when launching an service using the CLI:

```
$ tutum apps run --autodestroy ALWAYS [...] 
```

If not provided, it will have a default value of **OFF**.

###**Using the web interface[](https://docs.tutum.co/features/autodestroy/#launching-an-application-with-autodestroy-activated-through-the-ui "Permalink to this headline")** 

At the moment, activating the **Autodestroy** setting on
the **Application configuration** step of the **Launch new
application**wizard sets the *autodestroy* setting to **ALWAYS**.

![](http://s.tutum.co.s3.amazonaws.com/support/images/service-wizard-autodestroy.gif)

The default value is to be *deactivated* which will set it to **OFF**.

##**Activating Autodestroy to an already deployed service[](https://docs.tutum.co/features/autodestroy/#activating-autodestroy-to-an-already-deployed-application "Permalink to this headline")**

### **Using the API[](https://docs.tutum.co/features/autodestroy/#using-the-api "Permalink to this headline")**

You can set the autodestroy option after the service has been
deployed through the API:

```
PATCH /api/v1/service/(uuid)/ HTTP/1.1 
{ 
	"autodestroy": "ALWAYS" 
} 
```
See [*Update a
cluster*](https://docs.tutum.co/v2/api/?http#update-an-existing-node-cluster) for more
information.

### **Using the CLI[](https://docs.tutum.co/features/autodestroy/#using-the-cli "Permalink to this headline")** 

You can set the autodestroy option after the service has been
deployed using the CLI:

```
$ tutum apps set --autodestroy ALWAYS (name or uuid) 
```

### **Using the web interface[](https://docs.tutum.co/features/autodestroy/#using-the-web-interface "Permalink to this headline")**

You can also activate or deactivate **Autodestroy** to an service
after it has been deployed from within the service detail page.

![](http://s.tutum.co.s3.amazonaws.com/support/images/service-autodestroy-enable-disable.gif)

You can click on the **Autodestroy** button to turn the
feature **ON** or **OFF**. The behaviour of this settings is the same as
activating it on the **service configuration** step of the **Launch
new service** wizard.
