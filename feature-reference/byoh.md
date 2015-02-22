# Introduction

As well as deploying and managing hosts on the supported cloud providers, Tutum can use any Linux host as a node to deploy containers to. For this, we need you to install our **Tutum Agent**, which will allow Tutum to remotely manage your host.

## Bringing your own node

Go to the **Node dashboard** and click on **Bring your own node**.

![](https://s.tutum.co/support/images/node-byoh-wizard.png)

A command will be generated which includes a unique token tied to your account for node registration. Just execute this command in your Linux host  and **Tutum Agent** will be installed and configured.

If the installation and registration is successful, the web UI will change showing the new node FQDN:

![](https://s.tutum.co/support/images/node-byoh-wizard-finished.png)

The node is now ready to accept container deployments!


## Using the CLI to bring your own node

You can generate the command needed to install and configure the **Tutum Agent** by executing:

	$ tutum node byo
	
You will get the command that you have to use to bring your own node, including the token:

```
Tutum lets you use your own servers as nodes to run containers. For this you have to install our agent.
Run the following command on your server:

	curl -Ls https://files.tutum.co/scripts/install-agent.sh | sudo sh -s 63ad1c63ec5d431a9b31133e37e8a614
```

Execute this command in your host and it will appear in the list of nodes automatically.

## Uninstalling tutum-agent

To uninstall `tutum-agent` from your host, execute the following command:

```
$ apt-get remove tutum-agent
```

# Known limitations

## Firewall requisites

At the moment, in order for Tutum to connect to the Docker daemon in the node, we need ports **2375/tcp** (docker server), **6783/tcp** and **6783/udp** (overlay network), and **48001/tcp** (metrics) open in any firewalls your host might have enabled.

Of course, you will need to open any ports that you are planning to publish in your services. If you are using dynamic ports, Docker will assign them in the range **49153** to **65535** sequentially.

## Supported Linux distros

At the moment, **Tutum Agent** has only been tested in Ubuntu 14.04. We are working to make it available to more platforms soon.

## Running Docker with BYON

Simply use `docker` as you would otherwise. For example, running `$ docker ps` will show you a list of containers running. **Please note** there will be containers running from images starting with `tutum/` which you may not recognize. These are `system containers` that Tutum runs to offer its service. All of these come from open source repositories available at [http://www.github.com/tutumcloud](http://github.com/tutumcloud).

## Terminating and re-adding a node

If you remove a BYO-node from within Tutum, and then execute the Tutum Agent install script again, you'll see that the node does not reappear in the interface.

In order to add a node that was previously terminated, you have to SSH into the node and remove the `tutum-agent.conf` file. To do so, execute the following command prior to running the installation script again.

	$ rm /etc/tutum/agent/tutum-agent.conf

This is a known issue that will be fixed soon. From thereon manual deletion of `tutum-agent.conf` will not be required.




