# Introduction

Tutum allows you to upgrade the Docker server on your node when new versions are released and tested to work with our service. Because Docker currently requires containers to be restarted when it is upgraded to a new version, we don't automatically upgrade your nodes - we allow you to choose when you want to do it so you can plan it appropiately.

## Upgrading Docker in a node

Go to the detail page of the node that you would like to upgrade. On the left side you will see a **Docker Info** section:

![](https://s.tutum.co/support/images/node-detail-dockerupgrade.png)

If there is a new version available, a warning sign will be shown next to the docker version and an **Upgrade Docker** button will appear. Click on it to start the upgrade process.

After upgrading Docker, containers with the *autorestart* flag enabled will be automatically started. All other containers will be left in *stopped* state.


# Upgrading nodes using the API and CLI

Check our [API and CLI documentation](https://docs.tutum.co/v2/api/#upgrade-docker-daemon34) for more information on how to upgrade nodes with our API, SDKs and the CLI.


# Known issues

## Nodes using devicemapper driver

If your node has containers running and it's using the *devicemapper* graph driver, we are unable to upgrade it at this time. This is due to a known issue with *devicemapper* failing to start containers after a Docker restart. In this case, you have to terminate all containers on the node before starting the upgrade process. The upgrade process will automatically install the *AUFS* graph driver which doesn't have this issue.