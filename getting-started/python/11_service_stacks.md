## Service Stacks

A stack is a logical grouping of related services that are usually deployed together and require each other to work as intended. If you are familiar with *fig* or *Docker Compose* then you should feel right at home with **stacks**. Learn more about stacks [here](https://support.tutum.co/support/solutions/articles/5000569899-stacks). 

Stacks can be defined using a YAML file. The reference for the YAML definition is available [here](https://support.tutum.co/support/solutions/articles/5000583471-stack-yaml-reference). And the API documentation for Stacks is available [here](https://docs.tutum.co/v2/api/?http#stacks).

The three services that you created earlier form a stack with 3 services: the load-balancer, the web application and the redis cache. Checkout the file /quickstart-python/tutum.yml to see the stack file that defines the 3 services (lb, web, redis) you created in the previous steps, including all modifications and environment variables. 

This is what `tutum.yml` the file looks like:

```
lb:
  image: tutum/haproxy
  autorestart: always
  links:
    - web
  ports:
    - "80:80"
  roles:
    - global
web:
  image: tutum/quickstart-python
  autorestart: always
  links:
    - redis
  environment:
    - NAME=Python users!
  deployment_strategy: high_availability
  target_num_containers: 4
redis:
  image: tutum/redis
  autorestart: always
  environment:
    - REDIS_PASS=password
    - REDIS_APPENDONLY=yes
    - REDIS_APPENDFSYNC=always
```

### Running a stack

Running a stack only requires one command to be executed in the path containing your Stackfile.yml:

```
$ tutum stack up
```

Alternatively, you can specify the YML file to use and its location:

```
$ tutum up -f /usr/tutum/quickstart-python/tutum.yml
```