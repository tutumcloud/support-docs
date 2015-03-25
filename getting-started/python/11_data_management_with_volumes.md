## Data management with Volumes

The way the Redis setup was perfomed in the previous step, if the container were to crash, or if you were to redeploy the service, the data would be lost. But what if you wanted to persist data beyond the life of a container? Or, what if you wanted to share data from one container to another? Volumes let you do just that.

### Data persistence 

For Tutum to persist data, the data needs to live in a volume that is either defined on the image (ie. Dockerfile) or specified when creating a new service using Tutum. Learn more about volumes in Tutum [here](https://support.tutum.co/support/solutions/articles/5000520731-volumes).  

#### Test for lack of persistence

If you redeploy the Redis service you created earlier, you'll see that the counter is lost. Try that by executing the following command:

``` 
$ tutum service redeploy redis
```

Wait until the new container is running again:

```
$ tutum container ps --service redis
NAME     UUID      STATUS        IMAGE                RUN COMMAND      EXIT CODE  DEPLOYED        PORTS
redis-1  5ddc0d66  ✘ Terminated  tutum/redis:staging  /run.sh                  0  15 minutes ago  6379/tcp
redis-1  3eff67a9  ⚙ Starting    tutum/redis:staging  /run.sh
```

Once the container is running. Try curling or visiting the web endpoint again: 

    $ curl lb-1.$TUTUM_USER.cont.tutum.io:80
    <h3>Hello Python users!!</h3><b>Hostname:</b> web-1<br/><b>Visits:</b> 1%

The Redis cache service redeployment caused the counter to reset. 

#### Enabling persistence

Luckily for you the Redis image that you are using *tutum/redis* supports data persistence. Since data persistence is not a common requirement for a Redis cache, it's not enabled by default. To activate this functionality a couple of environment variables need to be defined to set it up. Let's do this!

```
$ tutum service set \
-e REDIS_APPENDONLY=yes \
-e REDIS_APPENDFSYNC=always \
redis --redeploy
```
This command defines two new environment variables in the **redis** service and redeploys it. Learn more about `tutum/redis` [here](https://github.com/tutumcloud/tutum-docker-redis). 

Redis will now create and store its data in a volume. The volume is in `/data`. 

Visit the web endpoint a number of times again, to make sure that everything is working as expected. Then redeploy the Redis service to see the counter persist even as the existing container is terminated, and a new one is created. 

    $ curl lb-1.$TUTUM_USER.cont.tutum.io:80
    <h3>Hello Python users!!</h3><b>Hostname:</b> web-1<br/><b>Visits:</b> 1%
    $ curl lb-1.$TUTUM_USER.cont.tutum.io:80
    <h3>Hello Python users!!</h3><b>Hostname:</b> web-2<br/><b>Visits:</b> 2%
    $ curl lb-1.$TUTUM_USER.cont.tutum.io:80
    <h3>Hello Python users!!</h3><b>Hostname:</b> web-3<br/><b>Visits:</b> 3%  
    $ tutum service redeploy redis
    897c435a-3d56-4c9d-8fd2-20a1be03a25f
    $ tutum container ps --service redis
    NAME     UUID      STATUS        IMAGE                RUN COMMAND      EXIT CODE  DEPLOYED        PORTS
    cache-1  8193cc1b  ✘ Terminated  tutum/redis:staging  /run.sh                  0  10 minutes ago  6379/tcp
    cache-1  61f63d97  ▶ Running     tutum/redis:staging  /run.sh                     37 seconds ago  6379/tcp
    $ curl lb-1.$TUTUM_USER.cont.tutum.io:80
    <h3>Hello Python users!!</h3><b>Hostname:</b> web-3<br/><b>Visits:</b> 4%  
    
Congratulations! You have achieved data persistence using Tutum!

### Sharing/reusing data volumes between services

A service's volume can be accessed by another service. To do this you use the `--volumes-from` flag when creating a new service. 

There are a number of use cases why you'd like to do this. For example, you can use this functionality to share data between two services, or to backup, restore, or migrate a volume to a local host or a cloud object storage (like AWS S3). 

Let's see how you'd go about downloading the `/data` volume from Redis to your local host using SCP (secure copy) utility.

First, run a SSH service that mounts the volumes of the redis you want to backup:

```
$ tutum service run -n download -p 22:2222 -e AUTHORIZED_KEYS="$(cat ~/.ssh/id_rsa.pub)" --volumes-from redis tutum/ubuntu
``` 

Then run **scp** to download the files of the data volume in Redis:

```
$ scp -r -P 2222 root@downloader-1.$TUTUM_USER.svc.tutum.io:/data .
```

You will now have a backup of the Redis data in your local host machine :)


Next: [Service Stacks](https://support.tutum.co/support/solutions/articles/5000539711)