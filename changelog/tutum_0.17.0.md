# Tutum 0.17.0

## Added 

- **[Packet](http://packet.net)** is now a supported infrastructure provider in Tutum. Packet offers a premium bare metal cloud designed for performance. [Sign up](https://app.packet.net/#/registration) using promo code **TUTUM100** for a $100.00 credit. With the addition of Packet, Tutum now provides native integration with 5 top IaaS providers, and more coming soon :) 
 
- **Stack name now shown in service list view** to help you figure out which service is which. More updates to help organization of all your services and stacks are on the pipeline, stay tuned! 

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.17.0/stackname_in_service_list.png)

- **Build auto-tagging** – with this new feature, when a tag (or GitHub release) is created on a branch which has *autobuild* enabled, a new build will be automatically triggered and the resulting image will be pushed to that docker repository using the git tag name as the repository tag.

- **Build retry action** for those pesky builds giving you a headache. 

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.17.0/build_retry.png)

- **Repository tag view** - see all of the tags associated with a repository right from within Tutum. If the repository is stored in the Tutum registry, you can now delete individual tags. 

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.17.0/tag_list.png)

- The Docker compose keys `working_dir`, `pid`, and `net` are now supported in Stackfiles. More info [here](https://tutum.freshdesk.com/support/solutions/articles/5000583471)

- **BYON (bring-your-own-node) support for Red Hat Enterprise Linux 7:** - with this update Tutum now officially supports BYON running Ubuntu 14.04 & 15.04, CentOS 7, Fedora 21 & 22, Debian 8, and Red Hat Enterprise Linux 7. Stay tuned, more coming soon. More info [here](https://github.com/tutumcloud/tutum-agent)


## Changed/Updated

- **Docker 1.7.1 upgrade** – after some [issues with Docker 1.6](http://blog.tutum.co/2015/07/28/docker-engine-in-tutum-a-tale-of-three-versions/) we are now back in full force with Docker 1.7.1. This update resolves most, if not all, memory leakage issues that you may have experienced to date. It also comes with many other fixes and enhancements. Click here to get the entire scoop for [Docker 1.7.0](https://github.com/docker/docker/blob/master/CHANGELOG.md#170-2015-06-16) and [Docker 1.7.1](https://github.com/docker/docker/blob/master/CHANGELOG.md#171-2015-07-14). You can upgrade all nodes simultaneously or individually. Please note that the overlay network will not work between nodes running 1.5.0 and 1.7.1. All new nodes will be provisioned using version 1.7.1. Click [here to upgrade now](https://dashboard.tutum.co/node/cluster/list/)

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.17.0/0.17.0.png)

- **Overlay network upgrade** to Weave 1.0.1 (latest estable) is bundled with the Docker 1.7.1 node upgrade. Find out what's new in the changelog for [Weave 1.0.0](https://github.com/weaveworks/weave/releases/tag/v1.0.0) and [Weave 1.0.1](https://github.com/weaveworks/weave/releases/tag/v1.0.1).

- **Stacks API endpoint** no longer expands services within the stacks. Now they are referenced by `resource_uri`. More info [here](https://docs.tutum.co/v2/api/?http#stacks)

## Fixed

- **Repositories in Tutum Registry** – when removing a repository stored in Tutum Registry, the internal reference to the repository is now removed, and the repository data is purged.

- **Speed enhancements** for faster service deployments, scaling, stopping, terminating. 

- **Stability optimizations** to minimize number of failed actions, and to increase consistency in the quality of service throughout the application and to all users. 
