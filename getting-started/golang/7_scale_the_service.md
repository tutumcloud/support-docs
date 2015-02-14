## Scale the service

Right now, your service is running on a single container. 

You can check how many containers are running using the `container ps` command:

```
$ tutum container ps --service web
NAME                   UUID      STATUS     IMAGE                                          RUN COMMAND          EXIT CODE  DEPLOYED     PORTS
web-1                  6c89f20e  ▶ Running  tutum.co/golang-user/quickstart-go:latest  python app.py                   1 hour ago   web-1.golang-user.cont.tutum.io:49162->80/tcp
```

`--service web` is used as a filter to only display those containers that are part of the *web* service.

Having only a single container running could become a problem if that container were to become unresponsive. To avoid this, you can scale to more than one container. You do this with the `service scale` command:

```
$ tutum service scale web 2
```

You'll now see that your service is scaling:

```
$ tutum service ps
NAME                 UUID      STATUS     IMAGE                                          DEPLOYED
web                  68a6fb2c  ⚙ Scaling  tutum.co/golang-user/quickstart-go:latest  1 hour ago
```

And that you have multiple containers:

```
$ tutum container ps --service web
NAME    UUID      STATUS     IMAGE                                      RUN COMMAND      EXIT CODE  DEPLOYED       PORTS
web-1   1fe3a0a2  ▶ Running  tutum.co/borjaburgos/quickstart-go:latest                              6 minutes ago  web-1.borjaburgos.cont.tutum.io:49176->80/tcp
web-2   5d5c7b42  ▶ Running  tutum.co/borjaburgos/quickstart-go:latest                              6 seconds ago  web-2.borjaburgos.cont.tutum.io:49163->80/tcp
```

Please note that containers don't get a *PORT* assigned until they are *running*.

From the example above (note that your URLs will be different) visiting (in the browser or curl) [web-1.golang-user.cont.tutum.io:49176](web-1.golang-user.cont.tutum.io:49176) will hit the first container, and [web-2.golang-user.cont.tutum.io:49163](web-2.golang-user.cont.tutum.io:49163) will hit the second container. 

    $ curl web-1.$TUTUM_USER.cont.tutum.io:49176
    <h1>hello, Golang users</h1>
    <b>Hostname: </b>web-1<br><b>MongoDB Status: </b>Not available%
    $ curl web-2.$TUTUM_USER.cont.tutum.io:49163
    <h1>hello, Golang users</h1>
    <b>Hostname: </b>web-2<br><b>MongoDB Status: </b>Not available%

Congratulations! You now have **two** containers running in your **web** service.

Next: [View logs](https://tutum.freshdesk.com/support/solutions/articles/5000559796)