## Overview 

You can register your SoftLayer account credentials in your Tutum account
to deploy **nodes** using Tutum's
Dashboard/API/CLI. Your SoftLayer username and API key are required in order to
have Tutum interact with SoftLayer on your behalf to create
and manage your **nodes** (virtual servers).

## Add SoftLayer Account Credentials

To add access to SoftLayer so that you can launch **nodes** from Tutum,
navigate to **Account info \> Cloud Providers**. Click **Add
credentials**.

![](https://s.tutum.co/support/images/link-softlayer-account.png)

A modal will be shown that will require for you to input
the `Username` and the `API Key`. If you do not have or know the correct SoftLayer credentials, or would like to create a `tutum` user, please read the next section.

### Create tutum user in SoftLayer

Although any SoftLayer account with the right privileges will work, we
recommend creating a new **tutum** user. 

Click here to access the **Users** section in SoftLayer: [https://control.softlayer.com/account/users](https://control.softlayer.com/account/users)

Click on **Add User**:

![](https://s.tutum.co/support/images/softlayer-step-1.png)

Fill in the **Add User - Profile** form, entering `tutum` in the username field, and making sure to fill in all other required fields. The passwords provided here are not irrelevant as Tutum will use the user's API key instead. Click on **Add User** when done.

![](https://s.tutum.co/support/images/softlayer-step-2.png)

In the next step, **Permissions**, select all **Devices**, **Network** and **Services** permissions, and click **Add Portal Permissions**:

![](https://s.tutum.co/support/images/softlayer-step-3.png)
![](https://s.tutum.co/support/images/softlayer-step-4.png)
![](https://s.tutum.co/support/images/softlayer-step-5.png)

Go back to the **Users** list, and click on the **Generate** link under the **API Key** column:

![](https://s.tutum.co/support/images/softlayer-step-6.png)

Once generated, click on the **View** link under the **API Key** column, and copy the generated API Key.

![](https://s.tutum.co/support/images/softlayer-step-7.png)


### Adding new SoftLayer credentials

Now that we have successfuly created the new user `tutum`, gotten its
credentials, and provided the user with enough permissions for Tutum to provision virtual servers on your behalf, we can go back to Tutum.

Copy and paste the `username` and the `API Key` you received from SoftLayer into their corresponding field in the modal shown in Tutum.

![](https://s.tutum.co/support/images/softlayer-modal.png)

You are now all set to start using SoftLayer as the infrastructure provider
for Tutum. Click [here to learn how to deploy your first node](https://support.tutum.co/support/solutions/articles/5000523221). 
