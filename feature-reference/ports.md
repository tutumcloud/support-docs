Tutum has the ability to **publish** or **expose** ports in services and containers, this in line with Docker's own functionality, as discussed here [here](https://docs.docker.com/reference/run/#expose-incoming-ports).

**Exposed ports** are ports that a container/service is listening to or on which it is providing a service. By default, in Tutum, exposed ports are only privately accessible. What this means is that only other services linked to the service exposing the ports will be able to communicate over the exposed port. 

Exposed ports cannot be accessed publicly over the internet. 

**Published ports** are exposed ports that are accessible publicly over the internet. Published ports are published to the node's (host's) public facing network interface in which the container is running.

Published ports CAN be accessed publicly over the internet.

## Launching a Service with a exposed port 

### Using the web interface

If the image that you are using for your service already exposes any ports, these will be reflected in Tutum in the **Launch new service** wizard.

After you select the image in the wizard, click on `Advanced options`. At the bottom you'll see a table of ports with the text **Click to modify image ports** overlayed. Click on it.

![](http://s.tutum.co.s3.amazonaws.com/support/images/exposing-port.png)

This image exposes port 80. Remember, this port will not be accesible publicly over the internet. Only other services that link this service will be able to access this exposed port. To add another port click on `Add Port`

### Using the API/CLI

Please reference our API and CLI documentation [here](https://docs.tutum.co/v2/api/#service) on how to launch a service with a exposed port. 

## Launching a Service with a published port

### Using the web interface

If the image that you are using for your service already exposes any ports, these will be reflected in Tutum in the **Launch new service** wizard.

After you select the image in the wizard, click on `Advanced options`. At the bottom you'll see a table of ports with the text **Click to modify image ports** overlayed. Click on it. 

To publish a port, simply click on the **Published** checkbox. Once you have done that you have the ability to choose to which port in the node (host) the port will be mapped to, or to have Tutum assign a port dynamically.

To access the published port over the internet, you will use the `Node port`.

![](http://s.tutum.co.s3.amazonaws.com/support/images/publishing-port.gif)

### Using the API/CLI

Please reference our API and CLI documentation [here](https://docs.tutum.co/v2/api/#service) on how to launch a service with a published port. 

## Checking which ports a service has exposed/published

### Using the web interface

In the **Service detail view**, on the left side of the screen, you can see a list of the ports that are exposed (private ports) represented by a lock symbol, as well as a list of the ports that are published (public ports) represented by an organization diagram/tree. 

Exposed ports are shown as: (**container port/proto**)

Published ports are shown as: (**node port**->**container port/proto**)

![](http://s.tutum.co.s3.amazonaws.com/support/images/exposed-and-published-ports.gif)

### Using the API/CLI

Please reference our API and CLI documentation [here](https://docs.tutum.co/v2/api/#service) on how to get a list of a service's exposed and published ports. 