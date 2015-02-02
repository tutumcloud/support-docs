In Tutum, you can define one or more data volumes for a service. **Volumes** are directories to hold reusable and shareable data (by the same service when it's redeployed, or by other services) which is stored outside of the container's filesystem and can persist when containers are terminated.


## Adding a data volume to a service

Data volumes can be either specified in the image's `Dockerfile` using the [`VOLUME` instruction](https://docs.docker.com/reference/builder/#volume), or when creating a service.

To define a data volume in a service, specify the **container path** where it should be created in the **Volumes** step of the **Create new service** wizard. Each container of the service will have its own volume. Data volumes are reused when the service is redeployed (data persists in this case), and deleted if the service is terminated.

![](https://s.tutum.co/support/images/data-volumes-wizard.png)

If you don't define a **host path**, a new empty volume will be created; otherwise, the specified **host path** will be mounted on the **container path**. In this case, you can specify whether to mount it read-only, or read/write.

![](https://s.tutum.co/support/images/host-volumes-wizard.png)


## Reusing data volumes from another service

If you want to reuse another service's data volumes, select a source service in the **Add volumes from** dropdown in the **Volumes** step of the **Create new service** wizard:

![](https://s.tutum.co/support/images/volumes-from-wizard.png)

All data volumes will be mounted on the same paths as in the source service. Also, the containers of the new service will be deployed to the same nodes where the source service containers are deployed (containers need to be on the same host in order to share volumes).

Note that a service with data volumes cannot be terminated until all services that are using its volumes are terminated.