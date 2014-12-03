## Introduction

In order to bring your own node (BYON), you need to have access to a running Ubuntu server.

You will need your **SSH Key** and a **Terminal**.

## Installing the Tutum Agent

Open the terminal and execute:

```chmod 400 name_of_ssh_key```

This changes permissions of your SSH key to *read only*.

Now you can connect to your running server:

```ssh ubuntu@ip_address -i name_of_ssh_key```

The BYON script needs root privileges so we'll execute: 

```sudo su```

Now, in the **"Nodes"** panel in Tutum, you will see a **"Bring your own node"** button.

Click this button and you will see a pop up modal with a command you must run.

```curl -Ls http://files.tutum.co.s3.amazonaws.com/scripts/install-agent-staging.sh | sudo sh -s 7bbf6d65d37e4eef9afd49533c3ce1f8```

!Image of Add your own server...

**Copy** and **paste** this command in your terminal with root privileges.

Head back to the Tutum **Bring your own node** pop up modal. In a few minutes the modal will confirm that the node has been registered. You can now manage containers in that node from Tutum!