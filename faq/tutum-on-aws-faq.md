## Which objects does Tutum create in my EC2 account?

The following objects will be created automatically by Tutum when deploying a node on AWS:

* An SSH keypair named `tutum-<uuid>`
* An EBS volume of type `gp2` with the size specified on the **Create new node cluster** wizard
* A security group named `tutum-default` with all ports open by default

By default, Tutum will try to deploy instances on EC2 using "EC2-Classic" or "EC2-VPC" using the default VPC for your account in the selected region. If there's no default VPC, Tutum will create the following additional objects:

* A VPC named `tutum-vpc` with the CIDR range `172.77.0.0/16`
* An internet gateway named `tutum-gateway` attached to `tutum-vpc`
* A subnet named `tutum-subnet` with the CIDR range `172.77.0.0/16` in `tutum-vpc`
* A route table named `tutum-route-table` in `tutum-vpc` associated with `tutum-gateway` and `tutum-subnet`
* A VPC security group named `tutum-vpc-default` with all ports open by default

In order for Tutum to detect these objects after they are created, it's important that **their names don't change**. Otherwise, Tutum will try to recreate them and fail due to conflicts.


## Can I modify the tutum-default security group?

You can change the ports opened in the `tutum-default` or `tutum-vpc-default` security groups as long as **ports 22/tcp (ssh), 2375/tcp (docker) and 48001/tcp (metrics)** are open. This is a temporary limitation that will be solved in the future.


## What happens if I restart a node in the AWS console?

After the node boots up, Tutum Agent will try contact our API and register itself with the new IP. We will update the DNS of the node and the containers on it to use the new IP automatically. The node should change its state from `Unreachable` to `Deployed`.

## Can I use an elastic IP for my nodes?

Yes, you can, but you will need to restart the Tutum Agent (or the host) for the changes to take effect in Tutum.


## Can I terminate a node from the AWS console?

If you created the node using Tutum and you terminate it in the AWS console, all data in that node will be destroyed, as the volume attached to it is set to destroy on node termination. If you haven't revoked your Tutum IAM user, we will detect the termination and will mark the node as `Terminated` on Tutum.

If you created the host yourself, added it to Tutum as a "Bring Your Own Node" and then terminated it, the node will stay in `Unreachable` state until you manually remove it.