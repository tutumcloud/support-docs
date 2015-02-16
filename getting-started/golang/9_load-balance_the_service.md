## Load-balance the service

To load-balance a service you need to deploy a load-balancing service that will distribute incoming requets to all of the available containers in the service. In this example, you need a loadbalancer that will forward incoming requests to both container #1 (web-1) and container #2 (web-2). For this, you will use [Tutum's HAProxy image](https://github.com/tutumcloud/tutum-docker-clusterproxy) to loadbalance, but other custom loadbalancers can also be used. 

```
$ tutum service run \
-p 80:80/tcp \
--role global \
--autorestart ALWAYS \
--link-service web:web \
--name lb \
tutum/haproxy
```
**-p 80:80/tcp** will publish port 80 of the container, and map it to port 80 of the node in which it will be deployed. **--role global** will grant API access to this service, this can be used to query the Tutum API from within the service, more info [here](https://support.tutum.co/support/solutions/articles/5000524639-api-roles). **--autorestart ALWAYS** restarts containers if they stop, more info [here](https://support.tutum.co/support/solutions/articles/5000012174-autorestart). **--link-service quickstart-go:web** links your loadbalancer service *haproxy* with the service *quickstart-go*, and this link is aliased *web*, more info [here](https://support.tutum.co/support/solutions/articles/5000012181-service-links). **--name lb** names the service *lb* (short for *loadbalancer*). And **tutum/haproxy** is the public image that we're using for this service. 

Execute the following to check if you service is already running:

```
$ tutum service ps
NAME    UUID      STATUS       #CONTAINERS  IMAGE                                      DEPLOYED        PUBLICDNS
web     1ecbf656  ▶ Running              2  tutum.co/golang-user/quickstart-go:latest  50 minutes ago  web.golang-user.svc.tutum.io
lb      1ca94183  ▶ Running              1  tutum/haproxy:latest                       1 minute ago    lb.golang-user.svc.tutum.io
```

Let's now check the container for this service. 
    
```
$ tutum container ps --service lb
NAME    UUID      STATUS     IMAGE                 RUN COMMAND      EXIT CODE  DEPLOYED      PORTS
lb-1    c3e3de06  ▶ Running  tutum/haproxy:latest  /run.sh                     1 minute ago  443/tcp, lb-1.golang-user.cont.tutum.io:80->80/tcp
```

You should notice an URL endpoint in the *PORT* column for lb-1. In the example above this is: [lb-1.golang-user.cont.tutum.io:80](lb-1.golang-user.cont.tutum.io:80). Try opening that in your browser or curl from the CLI. Refreshing or executing curl multiple times will show that requests are being distributed accross the two containers **web-1** and **web-2** running in the *web service*.

    $ curl lb-1.$TUTUM_USER.cont.tutum.io
    <h1>hello, Golang users</h1>
    <b>Hostname: </b>web-1<br><b>MongoDB Status: </b>Not available%
    $ curl lb-1.$TUTUM_USER.cont.tutum.io
    <h1>hello, Golang users</h1>
    <b>Hostname: </b>web-2<br><b>MongoDB Status: </b>Not available%

Find out more about *tutum/haproxy* [here](https://github.com/tutumcloud/tutum-docker-clusterproxy/).

Next: [Provision a data backend for your service](https://support.tutum.co/support/solutions/articles/5000539710)