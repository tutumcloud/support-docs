# Tutum 0.13.0

## Added 

- **Stacks Web UI + CLI:** a stack is a logical grouping of closely related services, that may be linked or interact with one another. If you already have fig or docker-compose templates, Tutum already supports them :) Learn more [here](https://support.tutum.co/support/solutions/articles/5000569899-stacks). Read our blog post on composability [here](http://blog.tutum.co/2015/03/10/container-composability-a-general-commentary-and-brief-overview/).

  ![](http://s.tutum.co.s3.amazonaws.com/support/images/stacks-ui.png)

- **Auto-redeploy on registry push:** you can now have Tutum automatically redeploy a service everytime its source private image is modified. This feature is only available to images stored in Tutum's private registry. For external images, you can use [webhooks](https://support.tutum.co/support/solutions/articles/5000513815-webhook-handlers). To make use of this feature, simply enable the *Autoredeploy* flag when creating or editing a service. Learn more [here](https://support.tutum.co/support/solutions/articles/5000569896-autoredeploy).

  ![](http://s.tutum.co.s3.amazonaws.com/support/images/autoredeploy_tutum_registry.png)
    
- **Single container redeploy:** users can now choose to redeploy a single container in a service. This functionality can be leveraged to achieve simple "red/black" type deployments using Tutum. 

  ![](http://s.tutum.co.s3.amazonaws.com/support/images/single_container_redeploy.png)

- **Container sync status flags in UI:** easily identify which containers are running an outdated service definition. 

  ![](http://s.tutum.co.s3.amazonaws.com/support/images/container-sync-flag.png)


   
- **Tutum CLI support for env_file:** read in a line delimited file of environment variables when creating/running/editing a service. Syntax is the same as Docker's CLI:

  `$ tutum service run --env-file myenvs.txt tutum/hello-world`
  
  ![](http://s.tutum.co.s3.amazonaws.com/support/images/env-file.png)

- **Tutum BYON Vagrant Box**: run your BYON Tutum node as a Vagrant box!

  ```
$ vagrant init tutum/node
$ TUTUM_TOKEN=<token> vagrant up
```
[More info](https://github.com/tutumcloud/tutum-node).

- **Tutum BYON Container**: run your BYON Tutum node inside a container!

  ```
$ docker run -d --net=host --privileged -e TUTUM_TOKEN=<token> tutum/node
```
[More info](https://github.com/tutumcloud/tutum-node).

## Changed

- **BYON behind NAT/firewall:** thanks to [secure introspectable tunnels](http://ngrok.com) it's now trivial to get your [BYON Tutum nodes](https://support.tutum.co/support/solutions/articles/5000513678-bring-your-own-node) running behind a NAT/firewall! This means you can now use Tutum to deploy containers to a VM running in your laptop without any complex config changes. 


## Fixed

- Squashed many bugs resulting in an increase in service stability. Thanks to all of the users that helped us by reporting these issues!