## Scale the service

Right now, your service is running on a single container. 

You can check how many containers are running using the `container ps` command:

```
$ tutum container ps
NAME                   UUID      STATUS     IMAGE                                          RUN COMMAND          EXIT CODE  DEPLOYED     PORTS
web-1                  6c89f20e  ▶ Running  tutum.co/python-user/python-quickstart:latest  python app.py                   1 hour ago   web-1.python-user.cont.tutum.io:49162->80/tcp
```

Having only a single container running could become a problem if that container were to become unresponsive. To avoid this, you can scale to more than one container. You do this with the `service scale` command:

```
$ tutum service scale web 2
```

You'll now see that your service is scaling:

```
$ tutum service ps
NAME                 UUID      STATUS     IMAGE                                          DEPLOYED
web                  68a6fb2c  ⚙ Scaling  tutum.co/python-user/python-quickstart:latest  1 hour ago
```

And that you have multiple containers:

```
$ tutum container ps
NAME                   UUID      STATUS      IMAGE                                          RUN COMMAND          EXIT CODE  DEPLOYED     PORTS
web-1                  6c89f20e  ▶ Running   tutum.co/python-user/python-quickstart:latest  python app.py                   1 hour ago   web-1.python-user.cont.tutum.io:49162->80/tcp
web-2                  ab045c42  ⚙ Starting  tutum.co/python-user/python-quickstart:latest                                               80/tcp
```

Please note that containers don't get a *PORT* assigned until they are *running*.

If you wait until the Service status goes from *Scaling* to *Running* you'll see that both containers get a *PORT* assigned to them. 

```
$ tutum container ps
NAME                   UUID      STATUS     IMAGE                                          RUN COMMAND          EXIT CODE  DEPLOYED      PORTS
web-1                  6c89f20e  ▶ Running  tutum.co/python-user/python-quickstart:latest  python app.py                   1 hour ago    web-1.python-user.cont.tutum.io:49162->80/tcp
web-2                  ab045c42  ▶ Running  tutum.co/python-user/python-quickstart:latest  python app.py                   1 minute ago  web-2.python-user.cont.tutum.io:49156->80/tcp
```

From the example above (note that your URLs will be different) visiting (in the browser or curl) [web-1.python-user.cont.tutum.io:49162](web-1.python-user.cont.tutum.io:49162) will hit the first container, and [web-2.python-user.cont.tutum.io:49156](web-2.python-user.cont.tutum.io:49156) will hit the second container. 

```
$ curl web-1.$TUTUM_USER.cont.tutum.io:49166
Hello Python Users!</br>Hostname: web-1</br>Counter: Redis Cache not found, counter disabled.%
$ curl web-2.$TUTUM_USER.cont.tutum.io:49156
Hello Python Users!</br>Hostname: web-2</br>Counter: Redis Cache not found, counter disabled.%
```

Congratulations! You now have two containers running in your **web** service.

Next: [View logs](https://tutum.freshdesk.com/support/solutions/articles/5000539708-8-view-logs)