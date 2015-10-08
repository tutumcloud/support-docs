# Tutum 0.18.0

## Added 

- **A new on-boarding experience** is now a available to new (and existing) users. Activate it by clicking on your picture in the top right corner, and then on "Welcome tour". 

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.18.0/onboarding.png)

- **Additional AWS native integrations** to support custom Virtual Private Clouds (VPC), Subnets, Security groups and Identity and Access Management (IAM). [Learn more](https://support.tutum.co/support/solutions/articles/5000526971-tutum-on-aws-faq)

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.18.0/aws-integrations.png)

- **Support for v2 external registries** has finally arrived. You requested and we listened. Here's the first step to v2 registries *everywhere*.

- **Autobuild checkbox** behavior in the UI has been fixed.

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.18.0/autobuild.png)

- **Build concurrency** on your nodes can now be controlled. Simply add a "tag" to your node in the format `builder=N` where N is the maximum number of parallel builds for that node, and Tutum will handle the rest. [Learn more](https://support.tutum.co/support/solutions/articles/5000638474-automated-builds)

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.18.0/build_parallel.png)

- **TUTUM_STACK_NAME** is now available as an environment variable to each of your containers belonging to a Stack. 

## Changed/Updated

- **Weave 1.0.3** is now being deployed to new nodes. This version of weave is backwards compatible with 1.0.1 and fixes some issues related to the overlay network.

- **Deprecated EC2 Classic** in favor of our new tight AWS integration with node cluster provisioning. [Learn more](https://support.tutum.co/support/solutions/articles/5000526971-tutum-on-aws-faq)

## Fixed

- Fixed a bug that prevented building different Docker images from the same Github repository.

- Fixed a bug that caused a node to become `unreachable` after its IP changed. 

- **Multiple enhancements and fixes to Tutum Agent** for all those pesky issues you've told us about. [Learn more](https://github.com/tutumcloud/tutum-agent)

- **Better error handling/messages throughout the app.** Nobody likes meaningless error messages that leave you clueless when something fails. We've gone through and improved them to be sweet and meaningful. 

- **Speed enhancements** for faster service deploying, scaling, stopping, and terminating. We're getting things ready for GA afterall ;)

- **Stability optimizations** to minimize the number of failed actions and to increase consistency in the quality of service throughout the application for all users. Yes, yes, yes, GA is coming. 
