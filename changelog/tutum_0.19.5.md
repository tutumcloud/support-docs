# Tutum 0.19.5

## Added

- **Docker 1.9.1-cs2:** Tutum now supports the latest commercially supported version of Docker. Click here to learn more about what's new in Docker [1.9](https://github.com/docker/docker/blob/master/CHANGELOG.md#190-2015-11-03) and [1.9.1](https://github.com/docker/docker/blob/master/CHANGELOG.md#191-2015-11-21). The inclusion of the commercially supported version of the engine in this release represents yet another step towards General Availability. 

  To update your nodes, simply click on the `Upgrade Docker in all nodes now` button in the [Node List View](https://dashboard.tutum.co/node/cluster/list/).
  
  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.19.5/node-update-1.9.1.png)
  
  Alternatively, you can update individual nodes from each of your node's Detailed View. 
  
  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.19.5/node-update-2-1.9.1.png)
  
  *Please be aware that performing a Docker Upgrade will momentarily stop your containers while the docker daemon is being updated.* 

- **Private networking:** why are my containers using my nodes' public IPs if all of my nodes are in the same private network? You asked, and we heard you loud and clear. With this release we've improved how the container overlay network is configured:
  - The overlay network will now prioritize using private IPs over public IPs when two nodes belong to the same private network. 
  - If these nodes are on the same VPC (Virtual Private Cloud) in AWS, the overlay network will make use of weave's new [_fast data path_](http://blog.weave.works/2015/11/13/weave-docker-networking-performance-fast-data-path/) to deliver network performance close to standard networking.
  
  *To take advantage of this new feature, please upgrade existing nodes to Docker 1.9.1-cs2 or re-deploy your containers to new nodes running Docker 1.9.1-cs2.*
  
## Changed/Updated

- **Tutum Builder** has been updated to use Docker 1.9.1 and Docker Compose 1.5.2. [Learn more](https://github.com/tutumcloud/builder) 