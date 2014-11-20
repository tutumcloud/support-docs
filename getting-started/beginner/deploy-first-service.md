Once you've deployed a [Node cluster](http://support.tutum.co/support/solutions/articles/5000012153-deploy-your-first-node) you can start deploying **Services**!

*What is a Service you may be wondering?*

Services are logical groups of containers from the same image. Services make it simple to scale your application across different nodes. Simply drag a slider to increase or decrease the availability, performance, and redundancy of your application.

**Let's get started!**

From the **Service dashboard** click on **Launch your first service**.

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001218590/original/Launch_your_first_service.png?1411924075)

Choose the **Image** you want to deploy. You can choose from one of our **Jumpstart** images to help get you started, or you can search thepublic **Docker Hub** images. If you have a **Private image** with Tutum, Docker, or another third party you can find them under the **Private images** tab. Remember you get a** private repository** with Tutum!

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001218653/original/Deploy_Jumpstart.png?1411924208)

You'll be taken to the **Service wizard** where you can change the **Service name**, choose the **Image tag**,**number of containers**, **Run command**, **Entrypoint**, and access **Advanced options** and set any **Environment variables** necessary. Clicking **Launch service** will automatically deploy the containers of your service to
the node with the least number of containers. We're currently working on our deployment algorithm and giving you even more customization over how you deploy your applications and services.

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001218670/original/Service_configuration.png?1411924315)

Once you've deployed your service, if it's a web application, you can visit your app by clicking on the **Web domain**. Here you can also see the container **Endpoints**, **Links**, **Logs**, **Environment variables**, and **Monitoring data**.

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001218676/original/Monitoring_logging_etc.png?1411924425)

Congratulations! You've officially launched your first service! For more
detail on deploying services, head over [here](https://support.tutum.co/support/solutions/articles/5000012184-docker-image).

Head over to our [Features](https://support.tutum.co/support/solutions/folders/5000046131) section to see what you can do with Tutum.

