## Overview 

You can link your Microsoft Azure account to your Tutum account to deploy **nodes** and **node clusters** using Tutum's Dashboard/API/CLI. Your Azure account is required in order to have Tutum interact with Azure on your behalf to create and manage your **nodes** (virtual machines).

## Link your Microsoft Azure account

Navigate to **Account info \> Cloud Providers**. You'll see a list of all the providers you can link your Tutum account to. Go ahead and click on the **Add credentials** button for Microsoft Azure:

![](https://s.tutum.co/support/images/azure-add-credentials2.png)

You'll be presented with the following screen:

![](https://s.tutum.co/support/images/azure-link-modal.png)

First, click on **Download management certificate** to download the public certificate generated for your Tutum account. Then, go to the **Azure Portal \> Settings (botton left corner) \> Management certificates tab \> ** and click on the **Upload** button on the bottom of the screen:
![](https://s.tutum.co/support/images/azure-portal-subscriptions.png)

In the **Upload a management certificate** dialog shown, select the previously downloaded certificate in the **File** field, and select the subscription that you want to use with Tutum:

![](https://s.tutum.co/support/images/azure-upload-certificate.png)

Once uploaded, copy the **subscription ID** (which looks like `aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee`), enter it in Tutum's **Azure credentials** dialog, and click **Save credentials**.

You are now all set to start using Microsoft Azure as the infrastructure provider for Tutum. Click [here to learn how to deploy your first node](https://support.tutum.co/support/solutions/articles/5000523221).