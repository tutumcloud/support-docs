## Overview 

You can register your [Packet](https://www.packet.net) account credentials in your Tutum account to deploy **nodes** and **node clusters** using Tutum's Dashboard/API/CLI. Your Packet API key is required in order to have Tutum interact with Packet on your behalf to create and manage your **nodes** (Packet devices).

## Add Packet credentials

To add access to Packet so that you can launch **nodes** from Tutum, navigate to **Account info \> Cloud Providers**. Click **Add credentials**.

![](https://s.tutum.co/support/images/add-packet-credentials.png)

A modal will be shown that will require for you to input the `Authentication token` to use. If you do not have one, please read the next section.


### Create Packet API key

Log into your Packet account, and click on **API Keys** on the left menu. Then, click on the **+** button on the bottom right corner of the screen, provide a description for your new API key, and click on **Generate**.

![](https://s.tutum.co/support/images/packet-add-apikey.png)

Copy the **Token** of the newly created API key and paste it in the `Authentication token` field of the `Packet credentials` modal in Tutum.


You are now all set to start using Packet as the infrastructure provider for Tutum. Click [here to learn how to deploy your first node](https://support.tutum.co/support/solutions/articles/5000523221). 
