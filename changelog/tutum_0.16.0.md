# Tutum 0.16.0

## Added 


- **Private repository list and detailed view added to web UI** - manage your private repositories from Tutum's Registry; this includes repositories added to Tutum from other registries (ie. Quay.io or DockerHub).

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.16.0/repository_dashboard.png)
  
- **Tutum Build** - build Docker images from your Github repos on your own infrastructure right from within Tutum. No more unpredictable build times or waiting forever in a queue; you’re in full control of your own Docker builds. 

	Enable **autobuild** to trigger a new Docker build with every **git push**. The best automation from your PaaS days, now available in a flexible, container-native platform. _And yes_, Bitbucket and Gitlab support IS coming. [Learn more](https://support.tutum.co/support/solutions/articles/5000638474)

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.16.0/build.png)

- **Autotest** - simple, yet powerful docker-friendly CI solution. Avoid the constraints of a traditional CI provider; maintain full control and reduce risk by using your own Docker images. [Learn more](https://support.tutum.co/support/solutions/articles/5000638476)

- **Official BYON support for Fedora and Debian** - This expands our official BYON support to Ubuntu, CentOS, Fedora and Debian. [Learn more](https://support.tutum.co/support/solutions/articles/5000513678-bring-your-own-node)

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.16.0/new_byon_support.png) 
    
- **Container and Service endpoints** - now shown in the **node** and **stack** detailed view. 

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.16.0/node_endpoints.png)
  
- **Monitoring jumpstarts** - New Relic is here, and we're already working on integrating Datadog and others! Stay tuned for upcoming enhancements to make configuring new services a breeze! More info [here](http://github.com/tutumcloud/newrelic-agent).

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.16.0/monitoring.png)

## Changed

- **Autorestart** - the UI now offers a 1:1 match to the more flexible API implementation. Select from the following options: `off`, `always`, `on failure`.

- **Autodestroy** - the UI now offers a 1:1 match to the Tutum API. Select from the following options: `off`, `always`, `on success`.

## Fixed

- **DNS issues resolved** - _finally_. For some time now, a few of you have experienced problems resolving service, container and node endpoints - mostly those using Linode, or Australian ISPs. Our interim solution was to use Google DNS (8.8.8.8 and 8.8.4.4). Today we are happy to say that we have found and fixed the issue! The culprit was DNS-0x20 encoding schemes not working with our DNS server. Interested in learning more? Check out this [research paper](http://courses.isi.jhu.edu/netsec/papers/increased_dns_resistance.pdf).
 
- Services using the `every node` deployment strategy now deploy new containers to nodes with matching tags as they become available.
