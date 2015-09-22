# Tutum 0.18.0

## Added 

- **A new on-boarding experience** is now a available to new (and existing) users. Activate it by clicking on your picture in the top right corner, and then on "Welcome tour". 

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.18.0/onboarding.png)

- **TUTUM_STACK_NAME** is now available as an environment variable to each of your containers belonging to a Stack. 

- **Additional AWS native integrations** to support custom Virtual Private Clouds (VPC), Subnets, Security groups and Identity and Access Management (IAM). [Learn more](https://support.tutum.co/support/solutions/articles/5000526971-tutum-on-aws-faq)

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.18.0/aws-integrations.png)

- **Autobuild UI checkbox** because autobuild isn't always the desired behaviour.

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.18.0/autobuild.png)

## Changed/Updated

- **Support for v2 external registries** has finally arrived. You requested and we listened. Here's the first step to v2 registries *everywhere*.

- **Deprecate EC2 Classic** in favor of our new tight AWS integration with node cluster provisioning. [Learn more](https://support.tutum.co/support/solutions/articles/5000526971-tutum-on-aws-faq)

## Fixed

- **Multiple enhancements and fixes to Tutum Agent** for all those pesky issues you've told us about. [Learn more](https://github.com/tutumcloud/tutum-agent)

- **Better error handling/messages throughout the app.** Nobody likes meaningless error messages that leave you clueless when something fails. We've gone through and improved them to be sweet and meaningful. 

- **Speed enhancements** for faster service deploying, scaling, stopping, and terminating. We're gettings things ready for GA afterall ;)

- **Stability optimizations** to minimize the number of failed actions and to increase consistency in the quality of service throughout the application for all users. Yes, yes, yes, GA is coming. 
