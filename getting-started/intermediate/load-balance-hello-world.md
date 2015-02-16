In order to load balance a web service that is deployed to multiple
containers we're going to need a proxy or load balancer. We'll show you
how to accomplish this using our **tutum/hello-world** as a sample web
service and our **jumpstart** image **tutum/haproxy** to load balance the
traffic. Traffic will be distributed across 8 containers in a node
cluster containing 4 nodes. We'll choose 4 x 512MB droplets from Digital
Ocean for each of our nodes.

##Creating a Node Cluster

Let's start off by deploying the node cluster of 4 nodes. Go to the
**Nodes** tab and click on **Launch new node cluster.**Choose the **node
cluster name**, **region, type/size**and**4**as the total **Number of
nodes**. If you have not linked your Digital Ocean credentials
yet, [click here for more info on how to do
this.](http://support.tutum.co/support/solutions/articles/5000012151)

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-node-wizard.png)

Click the **Launch node cluster** button. This operation may take up to
10 minutes while the nodes are provisioned, this a great time to grab a
coffee.

Once the node cluster is deployed successfully, with all 4 nodes we're
ready to proceed and launch our web service.

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-four-nodes.png)

##Launching the Web Service

Click on the **green popup message** that shows up, or click on the **Services** tab. And then on the **Create
service** button. From *Jumpstarts > Miscellaneous* select the image **tutum/hello-world**. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-hello-world-jumpstart.png)

You'll be taken to the Service configuration step of the wizard. Configure your service as per the screenshot below. Make sure to change the *deployment strategy* to **High Availability**, increase the *number of containers* to **8**, and add the *tag* **web** to ensure this service gets deployed to the right nodes. 

Lastly, because we will want to access these containers from the web, publicly, we must **publish port 80**. Click on the table and check the **Published** checkbox. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-wizard.png)

Click on **Create and deploy**.

After a short wait you'll be taken to the **Service View > Timeline.** Click on the **Containers** tab to see how your containers are quickly getting created and started.  

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-containers-start.png)

##Testing the Web Service

After at least one of your containers is in **Running** status, you can click on the **Endpoints** tab. Here you'll see a list of all the endpoints publicly available for this service. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-endpoints.png)

Click on the URL (it should look something like
http://web-1.username.cont.tutum.io:49154 ). This will
open a new tab on your web browser where you'll see
**tutum/hello-world**'s web page. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-hostname-1.png)


If you followed the same steps, but for another container in
**hello-world** web service you'll see that the hostname would change to match the container name (web-2, web-3, etc.).

##Launching the Load Balancer

Now that we've been able to verify the web service is working fine, go
back to the **Services** tab and click on **Launch new service** again.
This time around we're going to be launching a **load balancer**that
will be listening on **port 80** and balancing the traffic across the 8
containers that are running our web service. 

The load balancer is one of the **Jumpstart** images that Tutum
provides. You can find it in **Jumpstarts > Proxies >
tutum/haproxy.** Select the image and move on to the **Service
Configuration Screen.**

![](http://cdn.freshdesk.com/data/helpdesk/attachments/production/5001317900/original/Screen_Shot_2014-10-01_at_12.11.54_AM.png?1412136799)

We name the service *lb*, leave the tag, deployment startegy and number of containers with their default values. Then click on the ports table, check the *Published* checkbox and click the word *dynamic* to **modify the Node port from 80**. Screen should look like the screenshot below. Then click on the blue button that reads **Next:
environment variables.**

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-lb-conf.png)

Configuring the Load Balancer 
------------------------------

Ok, here's where things start getting interesting. First thing we need
to do is assign this service an API Role. You can [read more about API
Roles here](https://support.tutum.co/support/solutions/articles/5000012181).
Doing this will pass a *TUTUM_AUTH* environment variable to your
service's containers that will allow them to query Tutum's API on your
behalf. **tutum/haproxy** uses this to query the API on the status and
**number of web containers** that are part of the **web service** we
launched earlier.**HAproxy** uses this information to update its
configuration dynamically as your web service scales. 

Then we need to link our load balancing service with the web service
*web*. To do that select *web* (name may be different if you didn't name your service *web*) from the drop down list
of *Link services* and click on the blue button **+ Add. **

The link will appear in the table underneath. And your screen will look
like this:

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-lb-envvar.png)

You'll also notice that a lot of new environment variables are passed to
the new service we're about to launch. You can read more about
that [here](http://support.tutum.co/support/solutions/articles/5000012181-service).

Click **Create and deploy.**

## Testing the load-balanced Web Service

After launching the **HAproxy** image you are automatically taken to the
**Service view > Timeline.**

Once again, click on the the **endpoints** tab after the container **lb-1** is **Running**. Unlike with the web service, you'll see that this time the HTTP URL for the load balancer is mapped to port 80. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-lb-endpoint.png)

Click on the URL to open up a new tab on your browser. You'll see the
same webpage you saw earlier when checking the web service. This time
around though, try refreshing your web browser. With each refresh, you
should see the hostname change as your requests are load-balanced to different containers. 

![](http://s.tutum.co.s3.amazonaws.com/support/images/load-balance-web-lb.gif)

Each container running the web service gets a different hostname (container_name-#). The fact that with each refresh the hostname displayed changes means that our load balancer is working as expected. Each request is being load balanced to different containers! Note: if the hostname is not changing for you, try clearing your browser's cache or trying from a different web browser. 

Congratulations you have deployed your first load balanced web service
using Tutum!

## Bonus points: load balancing the load balancer (using DNS)

Now you may be asking, what if I scale the *lb* service to 2 or more containers? 

Tutum automatically assigns a DNS endpoint to all services that resolves to all of the containers of that service. You can use that DNS endpoint to load balance your load balancer. 

You can try it by pointing your web browser to *servicename.username.svc.tutum.io* or  using *dig* or *nslookup* to see how the service endpoint resolves.


