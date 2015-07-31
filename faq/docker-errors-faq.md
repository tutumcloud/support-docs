This is a list of known issues with current versions of docker along with our recommended workaround. You might encounter these errors in Tutum.


## Error message

*500 Server Error: Internal Server Error ("Cannot start container <id>: fork/exec /var/lib/docker/init/dockerinit-1.5.0: cannot allocate memory")*

*500 Server Error: Internal Server Error ("Cannot start container <id>: iptables failed: iptables --wait -t nat -A DOCKER -p tcp -d 0/0 --dport \<port> ! -i docker0 -j DNAT --to-destination \<ip>:\<port>:  (fork/exec /sbin/iptables: cannot allocate memory)")*

*Error pulling image (\<tag>) from \<image>, Untar fork/exec /usr/lib/tutum/docker: cannot allocate memory*

## Description

Your host has not enough free memory for docker to perform the required operation. If your containers are not responsible for the lack of free memory, it might be a known memory leak on the docker daemon < 1.7.0, which will be fixed in the yet-to-be-released docker 1.7.0.

## GitHub link

[docker/docker#12848](https://github.com/docker/docker/issues/12848)

## Workaround

Restart the `tutum-agent` service (`sudo service tutum-agent restart`) on the node, or restart the node.

---

## Error message

*500 Server Error: Internal Server Error ("Cannot stop container \<id>: [2] Container does not exist: container destroyed")*

## Description

After upgrading to docker 1.6.0, some containers cannot be stopped or terminated with the above error message.

## GitHub link

[docker/docker#12738](https://github.com/docker/docker/issues/12738)

## Workaround

Restarting the `tutum-agent` service (`sudo service tutum-agent restart`) on the node, or restarting the node, seems to solve the issue in some cases.

---

## Error message

*Get https://index.docker.io/v1/repositories/\<image>/images: dial tcp: lookup \<registry host> on \<ip>:53: read udp \<ip>:53: i/o timeout*

## Description

The DNS resolver configured on the host cannot resolve the registry's hostname.

## GitHub link

N/A

## Workaround

Retry the operation, or if the error persists, use another DNS resolver. Generally you can do this by updating your `/etc/resolv.conf` file with:

	nameserver 8.8.8.8
	nameserver 8.8.4.4

---

## Error message

*Driver aufs failed to create image rootfs \<id>: open /var/lib/docker/aufs/layers/\<id>: no such file or directory*

## Description

After upgrading docker, pulling images stops working with the above error message.

## GitHub link

[docker/docker#7554](https://github.com/docker/docker/issues/7554)

## Workaround

Trying to pull the same image after a few minutes solves the issue.

---

## Error message

*500 Server Error: Internal Server Error ("Cannot start container \<id>: Error getting container \<id> from driver devicemapper: Error mounting '/dev/mapper/docker-\<id>' on '/var/lib/docker/devicemapper/mnt/\<id>': device or resource busy")*

## Description

There are multiple _device or resource busy_ issues when using the "device mapper" storage driver, when starting and destroying containers.

## GitHub link

[docker/docker#5684](https://github.com/docker/docker/issues/5684)

## Workaround

Use AUFS (the default when installing the Tutum Agent) or another storage driver.

---

## Error message

*500 Server Error: Internal Server Error ("Cannot start container \<id>: Error starting userland proxy: listen tcp 0.0.0.0:\<port>: bind: address already in use")*

## Description

Tutum is trying to deploy a container publishing a port which is being used by a process on the host (like the SSH server listening in port `22`).

## GitHub link

N/A

## Workaround

Either choose another port, or SSH into the node and manually stop the process which is using the port that you are trying to use.

---

## Error message

*500 Server Error: Internal Server Error ("Cannot start container \<id>: Bind for 0.0.0.0:\<port> failed: port is already allocated")*

## Description

Tutum is trying to deploy a container publishing a port which is already used by another container outside of the scope of Tutum.

## GitHub link

N/A

## Workaround

Either choose another port, or SSH into the node and manually stop the container which is using the port that you are trying to use.

---

## Error message

*500 Server Error: Internal Server Error ("Cannot start container \<id>: [8] System error: exec: "\<path>": executable file not found in $PATH")*

## Description

The specified run command on the container does not exist on the container.

## GitHub link

N/A

## Workaround

Fix the run command on the service.

---

## Error message

*Timeout when pulling image from the registry*

## Description

Pulling the image is taking more than 10 minutes. It can be due to the docker daemon waiting for a nonexistent process pulling the required image.

## GitHub link

[docker/docker#12823](https://github.com/docker/docker/issues/12823)

## Workaround

Restarting the `tutum-agent` service (`sudo service tutum-agent restart`) on the node, or restarting the node, solves the issue.
