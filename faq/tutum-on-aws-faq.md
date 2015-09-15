# Tutum on AWS

## My accound does not link. How do I troubleshoot it?

To validate your AWS Security Credentials, Tutum tries to dry-run an instance on every region. Credentials will be valid if the operation succeedes at least in one of the regions. If you get the following message `Invalid AWS credentials or insufficient EC2 permissions` follow these steps to troubleshoot it:

1. [Download AWS CLI](https://aws.amazon.com/cli/) and [configure it](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) with your Security Credentials.
2. Run the following command:
 
        aws ec2 run-instances --dry-run --image-id ami-4d883350 --instance-type m3.medium

This will try to dry-run an Ubuntu 14.04 LTS 64-bit in `sa-east-1` (Sao Paulo, South America). You can look for the AMI in the region you want to deploy to [here](http://cloud-images.ubuntu.com/locator/ec2/). It should show you the error message. If everything is ok, you will see the following message:

    A client error (DryRunOperation) occurred when calling the RunInstances operation: Request would have succeeded, but DryRun flag is set.

## What is the difference between EC2-Classic & EC2-VPC?

According to [Amazon EC2 documentation](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-supported-platforms.html) there are two supported platforms to deploy your instances:

Platform | Introduced in | Description
------------ | ------------- | ------------
EC2-Classic | The original release of Amazon EC2  | Your instances run in a single, flat network that you share with other customers.
EC2-VPC | The original release of Amazon VPC | Your instances run in a virtual private cloud (VPC) that's logically isolated to your AWS account.

Quoting the same documentation:

    Your account may support both the EC2-VPC and EC2-Classic platforms, on a region-by-region basis. If you created your account after 2013-12-04, it supports EC2-VPC only. To find out which platforms your account supports, see Supported Platforms. If your accounts supports EC2-VPC only, we create a default VPC for you. A default VPC is a VPC that is already configured and ready for you to use. [...]
    
Tutum wanted to maintain compatibility with both platforms, so the steps to deploy a managed instance launched by Tutum were:

1. Create an SSH keypair named `tutum-<uuid>`.
2. Try to deploy the instance in Classic platform. If there is any kind of error with it (i.e. type of instance cannot be located without a VPC, like t2 instances) then try to deploy the instance in VPC platform.
3. In VPC platform, look for a VPC tagged with the name `tutum-vpc`. If exists, use it to deploy the instance. If not, create it and create any elements needed for the deployment (subnets, security groups, route tables, gateways).
4. Create an EBS volume of type `gp2` with the size specified on the **Create node cluster wizard** or with the parameter `disk` through the [API](https://docs.tutum.co/v2/api/#create-a-new-node-cluster). This disk will be used to store Docker containers and images.

Amazon does the following: in order to add a compatibility layer between Classic and VPC, for those accounts that only support VPC platform when you deploy an instance in Classic mode, it detects that your account does not support it but it does not complain. It will place it in the default VPC (with a default subnet) created in the region for you. So according to Tutum's behaviour, if your account only supports VPC, all your nodes get deployed in Amazon's default VPC.

In Tutum we believe VPC platform presents more benefits for the user than Classic, so we have decided to deprecate the deployment to Classic in favour of VPC. How does if affect to the deployments? there is no Classic step (#1), not anymore. Tutum will always look for a VPC tagged `tutum-vpc`. This way we provide a new level of customization: you are now able to define your own VPC in AWS portal, name it as `tutum-vpc` and deploy a node cluster in the region the VPC was created. Tutum will find it and use it! The rest of elements that Tutum needs for the deployment are also customizables. You can check their tag names in the following section.

## Which objects does Tutum create in my EC2 account?

If you decide to let Tutum create the needed elements for you, these are the details:

- VPC with the tag name `tutum-vpc` and CIDR range `10.77.0.0/16`.
- A set of subnets if there are no subnets already created in the VPC. Tutum will create a subnet in every Availability Zone (AZ) possible, and will leave enough CIDR space for the user to create customized subnets. Every subnet created is tagged with `tutum-subnet`.
- An internet gateway named `tutum-gateway` attached to the VPC.
- A route table name `tutum-route-table` in the VPC, associating the subnet with the gateway.

As part of the deprecation of Classic platform, users have now the ability to choose any of the elements explained above throught the API or the dashboard:

## How can I customize VPC/IAM elements in Tutum through dashboard?

In the launch node cluster view, you can choose:

- VPC dropdown:
    1. AUTO -> Delegates to Tutum the creation of the VPC.
    2. AUTO (tutum-vpc) -> Tutum's default VPC is already created, will use it for the deployments.
    3. "vpc-XXXX" -> You can select one of the VPCs already created by you.
- Subnets dropdown:
	1. AUTO -> Delegates to Tutum the management of the subnets. Will create them if they do not exist or will use the ones tagged with `tutum-subnet`.
	2. Multiple selection of existing subnets. See `How does Tutum balance my nodes among different availability zones?` section for detailed info.
- Security groups dropdown:
	1. AUTO
	2. Multiple selection of existing security groups.
- Instance profiles dropdown:
	1. None -> Tutum does not apply any instance profiles to the node.
	2. "my_instance_profile_name"

## How can I customize VPC/IAM elements in Tutum through API?

Add the following section to your body parameters:

```
"provider_options" = {
    "vpc": {                                                 # optional
        "id": "vpc-xxxxxxxx",                                # required
        "subnets": ["subnet-xxxxxxxx", "subnet-yyyyyyyy"],   # optional
        "security_groups": ["sg-xxxxxxxx"]                   # optional
    },
    "iam": {                                                 # optional
        "instance_profile_name": "my_instance_profile_name"  # required
    }
}
```

## How does Tutum balance my nodes among different availability zones? (high availability schema)

By default, Tutum will try to deploy your node cluster following an strategy of high availability. This means it will place every instance one by one in the less populated availability zone, for that node cluster. We can see this behaviour with some examples:

### We allow Tutum to manage VPC/subnets

Supose is the first time we deploy a node cluster with Tutum in a region, say Sao Paulo (South America, `sa-east-1`) and we delegate to Tutum the management of the deployment. Using the API, we do not sent any `provider_options`. Using the dashboard, we left VPC/subnet/security groups/IAM role values by default. Tutum will:

1. Look for a VPC called `tutum-vpc`. As it is our first time, it does not exist and will create it. Will create a `tutum-gateway` and will attach it to the VPC.
2. Retrieve all subnets in the VPC. As it is new, there are no subnets so it will create them. For every availability zone (AZ), Tutum will split the VPC CIDR IP space in (# of AZs + 1) blocks and will try to create (# of AZs) subnets (remember we left space for custom subnets). For every subnet, Tutum will try to dry-run an instance of the selected type and will create it if the operation succeedes, creating and associating a `tutum-route-table` to the subnet.
3. Once all subnets are created (note that there can be less subnets than AZs due to failures when dry-running the instances), Tutum will deploy every node of the cluster following a round-robin algorithm.

### Scaling a node cluster

Following the example described in the previous section, we have our node cluster deployed, and we want to scale it up. Tutum will:

1. Look for `tutum-vpc`. Found!
2. Look for `tutum-subnet`s. Found!
3. Count the nodes in every subnet. Now will choose the less populated subnet and will deploy the next node there.
4. Go to 3 until all nodes are deployed.

### We choose where to deploy

Supose we have another VPC for other purposes, with its components already created, and we want to deploy a node cluster in that VPC. Tutum will:

1. Look for the selected VPC. Found!
2. Look for selected subnets. If you do not select any subnets, Tutum will try to create them following the rules previously described.
3. If you have selected more than one subnet, Tutum will distribute the nodes in the cluster among those subnets. If not, all nodes will be placed in the same subnet.

## What happens if I restart a node in the AWS console?
After the node boots up, Tutum Agent will try contact our API and register itself with the new IP. We will update the DNS of the node and the containers on it to use the new IP automatically. The node should change its state from `Unreachable` to `Deployed`.

## Can I use an elastic IP for my nodes?
Yes, you can, but you will need to restart the Tutum Agent (or the host) for the changes to take effect in Tutum.

## Can I terminate a node from the AWS console?
If you created the node using Tutum and you terminate it in the AWS console, all data in that node will be destroyed, as the volume attached to it is set to destroy on node termination. If you haven't revoked your Tutum IAM user, we will detect the termination and will mark the node as `Terminated` on Tutum.

If you created the host yourself, added it to Tutum as a "Bring Your Own Node" and then terminated it, the node will stay `Unreachable` until you manually remove it.

## How do I SSH into the node?
Just follow [this article](https://support.tutum.co/support/solutions/articles/5000553071-sshing-into-a-tutum-node) to be able to access your nodes through SSH. If you have chosen a custom security group, remember to have port 22 opened!

## How do I backup my Docker container volumes to AWS S3?
[Dockup](https://github.com/tutumcloud/dockup) is an image developed to this purpose. You only need to run it taking the volumes of the container you want to backup with `volumes-from` and pass it the environment configuration of the container. You can find more info in its Github repo.