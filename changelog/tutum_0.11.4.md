# Tutum 0.11.4

## Added 
- **Service edit**: the ability to edit existing services. Editing capabilities include environment variables, links and service configuration (ie. run command, port mappings, etc.). Services must be redeployed after edit. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/edit-service.png)


- **Endpoints in service view**: a new tab in the service view to display all of the endpoints that a service is publishing.

![](http://s.tutum.co.s3.amazonaws.com/support/images/endpoints-feature.png)

- **Virtual host support**: the Tutum Jumpstart `tutum/haproxy` available under Jumptstarts > Proxies now supports virtual hosts. With virtual hosts, a single haproxy load-balancer can now balance traffic across multiple services. With this feature, multiple services can be accessible on the same port even when running on a single node. More information available [here](http://github.com/tutumcloud/tutum-docker-clusterproxy).

![](http://s.tutum.co.s3.amazonaws.com/support/images/haproxy_virtual_hosts.png)



## Changed
- **Docker 1.4.1**: new nodes will be provisioned using *Docker 1.4.1*. Old nodes can be upgraded to *Docker 1.4.1* from within Tutum. This feature is described [here](https://support.tutum.co/support/solutions/articles/5000515535-docker-upgrade). ![](http://s.tutum.co.s3.amazonaws.com/support/images/docker_1_4_1.png)


## Fixed

- Multiple bug fixes to increase stability of service. 