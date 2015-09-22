## Which objects does Tutum create in my Packet.net account?

Tutum will create a project named "Tutum" which will contain all the devices that Tutum deploys, no matter what type of device you chose.

Device storage is organized the following way:

- Type 1 devices has a RAID 1 of two SSD drives mounted in "/"
- Type 3 devices also has a RAID 1 of two SSD drives mounted in "/", and also offers two NVMe drives without being mounted. Tutum mounts a RAID 1 in "/var/lib/docker".

An SSH keypair named `tutum-<uuid>` will be created if no key is found in your account.

## How long does it take to deploy a Packet.net device?

Tutum deploys Ubuntu 14.04 LTS images on both types. Type 1 takes up to 5 ~ 10 min to be ready, while type 3 takes 8 ~ 13 min. Packet.net guys are working hard to reduce this deployment times.

## What happens if I restart a node in the Packet.net portal?

After the node boots up, Tutum Agent will try contact our API and register itself with the new IP. We will update the DNS of the node and the containers on it to use the new IP automatically. The node should change its state from `Unreachable` to `Deployed`.

## Can I terminate a node from the Packet.net portal?

If you created the node using Tutum and you terminate it in the portal, all data in that node will be destroyed. We will detect the termination and will mark the node as `Terminated` on Tutum.
If you turn off the device, Tutum will mark it as `Unreachable` because the node is not terminated but we cannot operate with it. 

If you created the host yourself, added it to Tutum as a "Bring Your Own Node" and then terminated it, the node will stay in `Unreachable` state until you manually remove it.

## How can I get into a Packet.net node managed by Tutum?

Packet.net copies SSH keys into the created device, so you can upload to Packet.net's portal your own SSH public key and then SSH into the node with the user `root`. You can also get into the node with Packet's console. You can also use a container to copy your SSH keys into the node, as explained in [https://support.tutum.co/support/solutions/articles/5000553071-sshing-into-a-tutum-node](https://support.tutum.co/support/solutions/articles/5000553071-sshing-into-a-tutum-node)

## Packet has returned an error, what can I do?

Here is a list of known errors thrown by Packet.net API:

- You have reached the maximum number of projects you can create (number). Please contact `help@packet.net` -> Packet.net accounts have a limit in the number of projects that can be created. Delete projects in your account or contact [Packet.net](https://www.packet.net/) support to increase the limit.
- There is an error with your Packet.net account. Please contact `help@packet.net` -> There is something wrong with your Packet.net account. Contact [Packet.net](https://www.packet.net/) for more details. 