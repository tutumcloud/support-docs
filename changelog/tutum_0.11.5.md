# Tutum 0.11.5

## Added 

- **Volumes**: directories to hold reusable and shareable data (by the same service when it's redeployed, or by other services) stored outside of the container's filesystem that can persist when containers are terminated. More info [here](https://tutum.freshdesk.com/support/solutions/articles/5000520731-volumes).

![](https://s.tutum.co/support/images/data-volumes-wizard.png)

- **Deployment strategies**: the ability to choose different scheduling algorithms when deploying containers to more than one node. Initially there are three strategies available: **emptiest node**, **high availability**, **every node**. Find out more information [here](https://tutum.freshdesk.com/support/solutions/articles/5000520721]).

![](http://s.tutum.co.s3.amazonaws.com/support/images/deployment_strategy.png)


## Changed

- **Tutum CLI v0.11.5**
  - filters: `tutum container ps --service servicename`
  - volumes: `-v --volume`, `--volumes-from`, `tutum volume/volumegroup list/inspect`
  - service public dns: `servicename.username.svc.tutum.io`

- **Docker client in BYON**: the `docker` binary is now in `$PATH` for BYON (bring-your-own-node) allowing you to easily execute docker commands locally. More [here](https://tutum.freshdesk.com/support/solutions/articles/5000513678-bring-your-own-node).


## Fixed

- Fixed issues when deploying to specific regions in DigitalOcean.
- Fixed issues with Azure integration.
- Node/container metric collection issues.
- Squashed *too many cookies* bug when using our Web UI.
- Multiple bug fixes to increase stability of service. 

## Known issues

- OAuth with Azure may not work for many users – we're working with Microsoft to resolve as soon as possible. 
