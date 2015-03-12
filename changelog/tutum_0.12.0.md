# Tutum 0.12.0

## Added 

- **Private overlay networking**: we have replaced our custom ambassador-based implementation for multi-container private networking and linking with a full-fledge private overlay network based on weave. All containers, regardless of host, cloud or datacenter, are assigned an IP and registered in a private network managed by Tutum. Among other benefits, this will result in faster [re]deployment times. Existing services must be redeployed to take advantage of this feature. Learn more in our [blog post](http://blog.tutum.co/2015/03/10/container-composability-a-general-commentary-and-brief-overview/).

![](http://s.tutum.co.s3.amazonaws.com/support/images/overlay_networking.png)

- **Dynamic links**: no more broken links! With this feature, links between services will never break, and best of all: no changes to your applications required! With Tutum's dynamic DNS service your app will *automagically* resolve hostnames of linked containers. For your applications, it works exactly the same as if it were running locally, but instead of resolving hostnames using `/etc/hosts`, Tutum will return the correct IP of the linked container. This works for envvar based links, and hostname based links. Worried about DNS caching in your app? Fret not, Tutum will ensure the same IPs are used when redeploying your services. Learn more [here](https://support.tutum.co/support/solutions/articles/5000012181-service-links).

![](http://s.tutum.co.s3.amazonaws.com/support/images/awesome_dyn_links.png)

- **Stacks API endpoint**: stacks are here! A stack is a logical grouping of closely related services, that may be linked or interact with one another. If you already have fig templates, Tutum will support them... we're working on our build capabilities :) Stacks will be available through our Web UI and CLI in the next release, but for now the API endpoint is ready for you to start using out this new feature. Documentation is available [here](https://docs.tutum.co/v2/api/?http#stacks).

Here's a sample stack in YAML:

```
lb:
  image: tutum/haproxy
  autorestart: always
  links:
    - "app:app"
  ports:
    - "80:80"
  tags:
    - prod
    - lb
  roles:
    - global
  environment:
    POLLING_PERIOD: 5
    MAXCONN: 512

app:
  image: tutum/quickstart-python:latest
  autorestart: always
  links:
    - "cache:redis"
  environment:
    NAME: awesome tutum users
  deployment_strategy: high_availability
  tags:
    - prod
    - app
  target_num_containers: 2

cache:
  image: tutum/redis
  autorestart: always
  environment:
    REDIS_PASS: password
  tags:
    - prod
    - cache
    
```


## Changed

- **Service redeploys**: when you redeploy a service, containers in that service will now be redeployed sequentially in order to minimize downtime. For example, when redeploying service **app** with 2 containers, the new sequence is: existing **app-1** *terminated* -> new **app-1** *running* -> existing **app-2** *terminated* -> new **app-2** *running*.

## Fixed

- Multiple bug fixes to increase stability of service. 

## Known issues

- We've resolved many of the issues with Azure, but a few problems remain. We're working with Microsoft to resolve this as soon as possible. 

