# Tutum 0.14.1

## Added 

- **New Community Chat**. Powered by Slack, where users and Tutum staff hang out to share information and help resolve issues and questions. Join from right within the app.

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/community_dashboard.png)


  ![](http://s.tutum.co.s3.amazonaws.com/changelog/slack.png)


## Changed

- **User-friendly container names**. Now, instead of using the container UUID as their docker name, Tutum sets it as `container-name[.stack-name].short-uuid`. This helps identify containers when external logging and monitoring systems are plugged directly to docker on the nodes.
- **Number of actions for any object limited to the most recent 100** to speed up the overall performance of the application. We will increase this limit in the future.

## Fixed

- **Public images cannot be added as private images**. We have added a check so users cannot add public images, such as the official images on the Docker Hub, as private images to their account.
- **Fixed deploy script on Softlayer**. Sometimes our deployment scripts were ran before the network was ready.
- Other bug fixes and stability improvements

## Known issues

- **Azure tokens expire every few hours**. We are working to change Azure account linking to be certificate-based instead of OAuth-based to avoid this limitation.


