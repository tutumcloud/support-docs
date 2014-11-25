**Crash recovery** is a Tutum feature that will autorestart and/or autoreplace your containers whenever they crash.

There are two settings related to crash recovery:

-   **Autorestart**: Tutum will try to autorestart the crashed container
    up to three times in a 1 minute period.
-   **Autoreplace**: Tutum will try to replace the crashed container
    with a new one up to three times in a 5 minute period.

Each of these settings have the following options:

-   **OFF**: if the container stops, regardless of the exit code, Tutum
    will not try to autorestart/autoreplace it.
-   **ON_FAILURE**: if the container stops with an exit code different
    from 0, Tutum will try to perform autorestart/autoreplace on it.
-   **ALWAYS**: if the container stops, regardless of the exit code,
    Tutum will try to perform autorestart/autoreplace on it.

If both **Autorestart** and **Autoreplace** are activated, Tutum will
try to perform **Autorestart** before **Autoreplace**.

If they fail to start the container after the number of tries during the
periods described above, they will leave the container
in **Stopped** state.

## **Launching a Service with Crash Recovery** 

###**Using the API**

You can specify the auto restart and autoreplace options when launching
a service through the API:

```
POST /api/v1/service/ HTTP/1.1 
{ 
	"auto restart": "ON_FAILURE", 
	"autoreplace": "ALWAYS", 
	[...] 
} 
```

If not provided, both are set to a default value of **OFF**. 

###**Using the CLI** 

You can specify the autorestart and autoreplace options when launching a
service using the CLI:

```
$ tutum service run --autorestart ON_FAILURE --autoreplace ALWAYS [...] 
```

If not provided, both are set to a default value of **OFF**. 

### **Using the web interface** 

At the moment, activating the **Crash recovery** setting on
the **Service configuration** step of the **Launch new service **wizard
sets both *autorestart* and *auto replace* settings to **ALWAYS**.

![](http://s.tutum.co.s3.amazonaws.com/support/images/service-wizard-crash-recovery.png)

The default value is to be *deactivated* which will set both options
to **OFF**.

## **Activating Crash Recovery to an already deployed service** 

### **Using the API** 
 
You can set the autorestart and autoreplace options after the service
has been deployed through the API:

```
PATCH /api/v1/service/(uuid)/ HTTP/1.1 
{ 
	"auto restart": "ON_FAILURE", 
	"autoreplace": "ALWAYS" 
} 
```

### **Using the CLI**

You can set the autorestart and autoreplace options after the
application has been deployed using the CLI:

``` 
$ tutum service set --autorestart ON_FAILURE --autoreplace ALWAYS (name or uuid) 
```

### **Using the web interface**

You can also activate or deactivate **Crash Recovery** to a service
after it has been deployed from within the service detail page.

![](http://s.tutum.co.s3.amazonaws.com/support/images/service-crash-recovery-enable-disable.gif)

You can click on the **Crash Recovery** button to turn the
feature **ON** or **OFF**. The behavior of this settings is the same as
activating it on the **Service configuration** step of the **Launch new
service** wizard.
