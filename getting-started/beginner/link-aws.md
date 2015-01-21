## Overview 

You have to register valid AWS credentials with your Tutum account
before you can deploy **nodes** and **node clusters** using Tutum's
Dashboard/API/CLI. Your AWS Security Credentials are required in order to
have Tutum interact with Amazon Web Services on your behalf to create
and manage your **nodes** (EC2 instances).

##Add AWS Account Credentials

To add access to AWS so that you can launch **nodes** in EC2 from Tutum,
navigate to **Account info \> Cloud Providers**. Click **Add
credentials**. A modal will be shown that will require for you to input
the `Access Key ID` and the `Secret Access Key`.

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001958626/original/Screen_Shot_2014-10-20_at_19.15.51.png?1413848730)

If you do not have or know the correct AWS credentials, or would like to
create a `tutum` user with AWS IAM (Identity and Access Management),
please read the next section.

Create tutum user in AWS IAM
----------------------------

Although any AWS credentials with the right privileges will work, we
recommend creating a new **tutum** user with AWS IAM. 

Click here to access the IAM panel in AWS: [https://console.aws.amazon.com/iam/\#users](https://console.aws.amazon.com/iam/#users)

Click on **Create New Users**, write `tutum` as the username, and make
sure to leave the checkbox **Generate an access key for each user**
checked. Click on **Create**.

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001958641/original/Screen_Shot_2014-10-20_at_19.23.33.png?1413848771)

You will then be shown the `Access Key ID` and `Secret Access Key`. Make
sure to copy both of these, or click on the **Download Credentials**
button, as these will not be shown again.

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001958660/original/Screen_Shot_2014-10-20_at_19.24.33.png?1413848800)

## Attach User Policy

Before Tutum can use the credentials we just created we need to provide
said credentials with some privileges to provision EC2 resources on your
behalf. 

To do this, go to **Users \> tutum** in the AWS IAM panel: [https://console.aws.amazon.com/iam/\#users](https://console.aws.amazon.com/iam/#users/tutum) 

Click on **Attach User Policy**. Then click on **Custom Policy**. Name
the policy `tutum-policy` and paste the following text in the space
provided for **Policy Document**.

```
{
  "Statement": [
    {
      "Action": "ec2:*",
      "Effect": "Allow",
      "Resource": "*"
    }
  ]
}
```

If you want to limit Tutum to a specific EC2 Region, you can use the following policy instead:

```
{
  "Statement": [
    {
      "Action": "ec2:*",
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

Click on **Apply Policy**.

### Adding new AWS credentials

Now that we have successfuly created the new user `tutum`, gotten its
credentials, and provided the user with a custom policy that will allow
Tutum to provision EC2 resources on your behalf, we can go back to
Tutum.

Copy and paste the `Access Key ID`and the `Secret Access Key` you
received from AWS into their corresponding field in the modal shown in
Tutum.

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001958672/original/Screen_Shot_2014-10-20_at_19.40.50.png?1413848821)

You are now all set to start using AWS as the infrastructure provider
for Tutum. Click [here to learn how to deploy your first node](https://tutum.freshdesk.com/support/solutions/articles/5000523221-your-first-node). 
