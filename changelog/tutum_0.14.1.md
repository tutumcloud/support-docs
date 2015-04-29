# Tutum 0.14.1

## Added 

- **New Community Chat** available powered by Slack, where users and Tutum staff hang out to share information and help resolve issues and questions.

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/slack.png)


## Changed

- **User-friendly container names**. Now, instead of using the container UUID as their docker name, Tutum sets `container-name[.stack-name].short-uuid` as their name. This helps identify containers when external logging and monitoring systems are plugged directly to docker on the nodes.
- **Number of actions for any object limited to the most recent 100** to speed up the overall performance of the application. We will increase this limit in the future.

## Fixed

- **Public images cannot be added as private images**. We have added a check so users cannot add public images, such as the official images on the Docker Hub, as private images to their account.
- **Fixed deploy script on Softlayer**. Sometimes our deployment scripts was ran before the network was ready.
- Other bug fixes and stability improvements

## Known issues

- **Azure tokens expire every few hours**. We are working to switch Azure account linking to be certificate-based instead of OAuth-based to avoid this limitation.

