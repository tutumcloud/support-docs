## Provision a data backend for your service

Tutum offers a large number of data stores in its *Jumpstart* library. From Redis and MongoDB to PostgreSQL and MySQL. In this step you will learn how to add a databackend that your service will use. You'll be creating a Redis cache, but most concepts will apply to any data backend.

The first step is to provision the data service itself. Execute this to create and run the Redis service using the [tutum/redis](https://github.com/tutumcloud/tutum-docker-redis) image:

```
$ tutum service run \
--env REDIS_PASS="password" \
--name redis \
tutum/redis
```
**--env REDIS_PASS="password"** defines an environment variable that sets the password for Redis. Because we are not publishing any ports for this service only services **linked** to your *Redis service* will be able to connect to it.     

Check to make sure that your *redis service* is *running*.

```
$ tutum service ps
NAME                 UUID      STATUS            IMAGE                                          DEPLOYED
redis                89806f93  ▶ Running         tutum/redis:latest                             29 minutes ago
web                  bf644f91  ▶ Running         tutum.co/python-user/python-quickstart:latest  26 minutes ago
lb                   2f0d4b38  ▶ Running         tutum/haproxy:latest                           25 minutes ago
```

### Link the Web (python) service to the Data (redis) service

```
$ tutum service set --link redis:redis --redeploy web
```

Visit or `curl` the load balanced web endpoint again. You'll notice that the `web service` now makes use of the Redis data backend to keep a counter that is in-sync with all of its containers. 

```
$ curl lb-1.$TUTUM_USER.cont.tutum.io
Hello World</br>Hostname: web-1</br>Counter: 1%
$ curl lb-1.$TUTUM_USER.cont.tutum.io
Hello World</br>Hostname: web-3</br>Counter: 2%
$ curl lb-1.$TUTUM_USER.cont.tutum.io
Hello World</br>Hostname: web-2</br>Counter: 3%
$ curl lb-1.$TUTUM_USER.cont.tutum.io
Hello World</br>Hostname: web-5</br>Counter: 4%
$ curl lb-1.$TUTUM_USER.cont.tutum.io
Hello World</br>Hostname: web-3</br>Counter: 5%
```

Next: [Data management with Volumes](https://support.tutum.co/support/solutions/articles/5000583708)