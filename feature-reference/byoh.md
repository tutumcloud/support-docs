# Introduction

As well as deploying and managing hosts on the supported cloud providers, Tutum can use any Linux host as a node to deploy containers to. For this, we need you to install our **Tutum Agent**, which will allow Tutum to remotely manage your host.

Please note that **Tutum Agent** comes with its own docker binary and will automatically remove any prior installation of the **docker.io** or **lxc-docker** packages when being installed. Please refer to the *Known Limitations* section below for more information.


## Bringing your own node

Go to the **Node dashboard** and click on **Bring your own node**.

![](https://s.tutum.co/support/images/node-byoh-wizard-v2.png)

A command will be generated which includes a unique token tied to your account for node registration. Just execute this command in your Linux host and **Tutum Agent** will be installed and configured.

If the installation and registration is successful, the web UI will change showing the new node hostname:

![](https://s.tutum.co/support/images/node-byoh-wizard-finished-v2.png)

The node is now ready to accept container deployments!


## Using the CLI to bring your own node

You can generate the command needed to install and configure the **Tutum Agent** by executing:

	$ tutum node byo
	
You will get the command that you have to use to bring your own node, including the token:

```
Tutum lets you use your own servers as nodes to run containers. For this you have to install our agent.
Run the following command on your server:

	curl -Ls https://get.tutum.co/ | sudo -H sh -s 63ad1c63ec5d431a9b31133e37e8a614
```

Execute this command in your host and it will appear in the list of nodes automatically.

## Uninstalling Tutum Agent

To uninstall `tutum-agent` from your host, execute the following command:

```
$ apt-get remove tutum-agent
```

## Upgrading Tutum Agent

To upgrade `tutum-agent` execute the following command from your BYON host:

```
$ apt-get update && apt-get install -y tutum-agent`
```

# Known limitations

## Firewall requisites

The following ports must be opened in any firewalls:

* **6783/tcp** and **6783/udp**: for the node to join the private overlay network for containers in other nodes.

The following ports are recommended to be opened in any firewalls:

* **2375/tcp**: for Tutum to communicate with the Docker daemon running in the node. If port 2375 is not accessible, Tutum will attempt to communicate with node through a secure tunnel. 

Of course, you will need to open any ports that you are planning to publish in your services. If you are using dynamic ports, Docker will assign them in the range **32768** to **61000** sequentially.

## Supported Linux distros

At the moment, **Tutum Agent** has only been tested in Ubuntu 14.04. We are working to make it available to more platforms soon.

## Installing Tutum Agent on a node with Docker already installed

If you install `tutum-agent` having already installed the `docker.io` or `lxc-docker` packages, `apt-get` will remove them prior to installing `tutum-agent`. This is due to the fact that `tutum-agent` comes with the `docker` binary already built in. The installation script will also try to install the kernel headers required for `AUFS` support.

* If you were already using the `AUFS` storage driver before installing `tutum-agent`, your existing containers and images will appear automatically after installing it.
* If you were using `devicemapper` or any other storage driver, and `AUFS` support was successfully installed (you can check this by running `docker info | grep Storage`), you won't be able to use your existing containers and images.


## Executing docker locally with Tutum Agent installed

Once you install the Tutum Agent, you can still use the `docker` command as you would otherwise. For example, running `docker ps` will show you a list of containers running.

**Please note** that there will be containers running from images starting with `tutum/` which you may not recognize. These are **system containers** that Tutum runs to offer its service. All of these come from open source repositories available at [GitHub](https://github.com/tutumcloud).





