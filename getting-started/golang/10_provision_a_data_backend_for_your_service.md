## Provision a data backend for your service

Tutum offers a large number of data stores in its *Jumpstart* library. From Redis and MongoDB to PostgreSQL and MySQL. In this step you will learn how to add a databackend that your service will use. You'll be creating a Mongo DB, but most concepts will apply to any data backend.

The first step is to provision the data service itself. Execute this to create and run the Mongo service using the [tutum/mongodb](https://github.com/tutumcloud/tutum-docker-mongodb) image:

```
$ tutum service run -e AUTH=no --name mongo tutum/mongodb
```
**--env AUTH=no** defines an environment variable that disables authentication for MongoDB. Because we are not publishing any ports for this service, only services **linked** to your *MongoDB service* will be able to connect to it.     

Check to make sure that your *mongo service* is *running*.

```
$ tutum service ps
NAME    UUID      STATUS       #CONTAINERS  IMAGE                                      DEPLOYED        PUBLICDNS
web     1ecbf656  ▶ Running              2  tutum.co/borjaburgos/quickstart-go:latest  1 hour ago      web.borjaburgos.svc.tutum.io
lb      1ca94183  ▶ Running              1  tutum/haproxy:latest                       13 minutes ago  lb.borjaburgos.svc.tutum.io
mongo   59e0f357  ▶ Running              1  tutum/mongodb:latest                       1 minute ago    mongo.borjaburgos.svc.tutum.io
```

### Link the Web (go) service to the Data (mongo) service

```
$ tutum service set --link mongo:mongo --redeploy web
```

Visit or `curl` the load balanced web endpoint again. You'll notice that the *web* service now makes use of the MongoDB data backend, and the *MongoDB Status* shows as **Connected**. Do not that both containers, **web-1** and **web-2**, make use of the same **mongo** service running a single container.

    $ curl lb-1.$TUTUM_USER.cont.tutum.io
    <h1>hello, Golang users</h1>
    <b>Hostname: </b>web-1<br><b>MongoDB Status: </b>Connected%
    $ curl lb-1.$TUTUM_USER.cont.tutum.io
    <h1>hello, Golang users</h1>
    <b>Hostname: </b>web-2<br><b>MongoDB Status: </b>Connected%
    $ curl lb-1.$TUTUM_USER.cont.tutum.io
    <h1>hello, Golang users</h1>
    <b>Hostname: </b>web-1<br><b>MongoDB Status: </b>Connected%
    $ curl lb-1.$TUTUM_USER.cont.tutum.io
    <h1>hello, Golang users</h1>
    <b>Hostname: </b>web-2<br><b>MongoDB Status: </b>Connected%

Next: [Service Stacks](https://support.tutum.co/support/solutions/articles/5000539711)