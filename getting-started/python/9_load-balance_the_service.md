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
**-p 80:80/tcp** will publish port 80 of the container, and map it to port 80 of the node in which it will be deployed. **--role global** will grant API access to this service, this can be used to query the Tutum API from within the service, more info [here](https://support.tutum.co/support/solutions/articles/5000524639-api-roles). **--autorestart ALWAYS** restarts containers if they stop, more info [here](https://support.tutum.co/support/solutions/articles/5000012174-autorestart). **--link-service quickstart-python:web** links your loadbalancer service *haproxy* with the service *quickstart-python*, and this link is aliased *web*, more info [here](https://support.tutum.co/support/solutions/articles/5000012181-service-links). **--name lb** names the service *lb* (short for *loadbalancer*). And **tutum/haproxy** is the public image that we're using for this service. 

Execute the following to check if you service is already running:

```
$ tutum service ps
NAME                 UUID      STATUS     IMAGE                                          DEPLOYED
web                  68a6fb2c  ▶ Running  tutum.co/python-user/quickstart-python:latest  2 hours ago
lb                   e81f3815  ▶ Running  tutum/haproxy:latest                           11 minutes ago
```

Let's now check the container for this service. 
    
```
$ tutum container ps
NAME                   UUID      STATUS     IMAGE                                          RUN COMMAND          EXIT CODE  DEPLOYED        PORTS
web-1                  6c89f20e  ▶ Running  tutum.co/python-user/quickstart-python:latest  python app.py                   2 hours ago     web-1.python-user.cont.tutum.io:49162->80/tcp
web-2                  ab045c42  ▶ Running  tutum.co/python-user/quickstart-python:latest  python app.py                   33 minutes ago  web-2.python-user.cont.tutum.io:49156->80/tcp
lb-1                   9793e58b  ▶ Running  tutum/haproxy:latest                           /run.sh                         14 minutes ago  443/tcp, lb-1.python-user.cont.tutum.io:80->80/tcp
```

You should notice an URL endpoint in the *PORT* column for haproxy-1. In the example above this is: [lb-1.python-user.cont.tutum.io:80](lb-1.python-user.cont.tutum.io:80). Try opening that in your browser or curl from the CLI. Refreshing or executing curl multiple times will show that requests are being distributed accross the two containers running in the *web service*

```
$ curl lb-1.$TUTUM_USER.cont.tutum.io
Hello World</br>Hostname: web-1</br>Counter: Redis Cache not found, counter disabled.%
$ curl lb-1.$TUTUM_USER.cont.tutum.io                                                                                                                                                
Hello World</br>Hostname: web-2</br>Counter: Redis Cache not found, counter disabled.%
```
Find out more about *tutum/haproxy* [here](https://github.com/tutumcloud/tutum-docker-clusterproxy/).

Next: [Provision a data backend for your service](https://support.tutum.co/support/solutions/articles/5000539710)