## Overview

You can register your AWS account credentials in your Tutum account to deploy **node clusters** and **nodes** using Tutum's dashboard/API/CLI. Your AWS Security Credentials are required in order to have Tutum interact with AWS on your behalf to create and manage your nodes (EC2 instances).
 
## Add AWS Account Credentials

To add access to AWS so that you can launch **nodes** in EC2 from Tutum,
navigate to **Account info \> Cloud Providers**. Click **Add
credentials**.

![](https://s.tutum.co/support/images/link-aws-account.png)

A modal will be shown that will require for you to input
the `Access Key ID` and the `Secret Access Key`. If you do not have or know the correct AWS credentials, or would like to create a `tutum` user with AWS IAM (Identity and Access Management), please read the next section.

## Create tutum user in AWS IAM

Although any AWS credentials with the right privileges will work, we
recommend creating a new **tutum** user with AWS IAM. 

Click here to access the IAM panel in AWS: [https://console.aws.amazon.com/iam/\#users](https://console.aws.amazon.com/iam/#users)

Click on **Create New Users**, write `tutum` as the username, and make
sure to leave the checkbox **Generate an access key for each user**
checked. Click on **Create**.

![](https://s.tutum.co/support/images/aws-iam-step-1.png)

You will then be shown the `Access Key ID` and `Secret Access Key`. Make
sure to copy both of these, or click on the **Download Credentials**
button, as these will not be shown again.

![](https://s.tutum.co/support/images/aws-iam-step-2.png)

## Attach User Policy

Before Tutum can use the credentials we just created we need to provide
said credentials with some privileges to provision EC2 resources on your
behalf. 

To do this, go to **Policies \> Create Policy** in the AWS IAM panel: [https://console.aws.amazon.com/iam/#policies](https://console.aws.amazon.com/iam/#policies) 

Click on **Create Your Own Policy**. Name
the policy `tutum-policy` and paste the following text in the space
provided for **Policy Document**.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "ec2:*",
        "iam:ListInstanceProfiles"
      ],
      "Effect": "Allow",
      "Resource": "*"
    }
  ]
}
```

`ec2:*` allows the user to perform any operation in EC2.

`iam:ListInstanceProfiles` allows the user to retrieve instance profiles to apply to your nodes.

If you want to limit Tutum to a specific EC2 Region, you can use the following policy instead (i.e. `us-west-2` US West (Oregon)):

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "ec2:*",
        "iam:ListInstanceProfiles"
      ],
      "Effect": "Allow",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "ec2:Region": "us-west-2"
        }
      }
    }
  ]
}
```

Click on **Validate Policy**. If everything is ok, then **Create Policy**.

After done this, return to Users > tutum in the AWS IAM panel: [https://console.aws.amazon.com/iam/#users](https://console.aws.amazon.com/iam/#users) and **Attach Policy**.

## Adding new AWS credentials

Now that we have successfuly created the new user `tutum`, gotten its
credentials, and provided the user with a custom policy that will allow
Tutum to provision EC2 resources on your behalf, we can go back to
Tutum.

Copy and paste the `Access Key ID`and the `Secret Access Key` you
received from AWS into their corresponding field in the modal shown in
Tutum.

![](https://s.tutum.co/support/images/aws-modal.png)

You are now all set to start using AWS as the infrastructure provider
for Tutum. Click [here to learn how to deploy your first node](https://support.tutum.co/support/solutions/articles/5000523221). 
