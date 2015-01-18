## Define environment variables

Docker lets you externalize configuration - storing data such as encryption keys or external resource addresses in environment variables. Tutum makes it easy to define, share, and update the environment variables of your services.

At runtime, environment variables are exposed to the application inside the container.

Open the file in quickstart-python/app.py, and take a look at the return statement in the method *hello()*:

```
return "Hello" + os.environ.get('NAME') + '!</br>' + "Hostname: " + socket.gethostname() + '</br>' + "Counter: " + str(counter)
```

You'll see that the code uses **os.environ.get('NAME')** to get the environment variable **NAME**. If you modify the enviroment variable, the message should change accordingly. Try that by executing:

```
$ tutum service set --env NAME="Python Users" --redeploy web
```

Execute `$ tutum container ps` again to get the new container endpoint. You'll see that there are now two `web-1` containers, one with a status of **terminated** and another one **starting** or **running**.

```
$ tutum container ps
NAME                         UUID      STATUS        IMAGE                                          RUN COMMAND      EXIT CODE  DEPLOYED        PORTS
web-1                        a2ff2247  ✘ Terminated  tutum.co/borjaburgos/quickstart-python:latest  python app.py               40 minutes ago  web-1.borjaburgos.cont.tutum.io:49165->80/tcp
web-1                        ae20d960  ▶ Running     tutum.co/borjaburgos/quickstart-python:latest  python app.py               20 seconds ago  web-1.borjaburgos.cont.tutum.io:49166->80/tcp
```
Now curl the new endpointto see the updated *Hello Python Users!* greeting. *Note: if you don't see an endpoint, wait until the container status changes to **running**.*

```
$ curl web-1.$TUTUM_USER.cont.tutum.io:49162
Hello Python Users!</br>Hostname: e360d05cdb81</br>Counter: Redis Cache not found, counter disabled.%
```

Your service now returns `Hello Python Users!`, good job on modifiying your service using environment variables!

### Environment Variables and the Dockerfile

Environment variables can be set in the Dockerfile, and modified at runtime (as you just did). 

If you are wondering where the default value for the **NAME** environment variable is set, checkout the file quickstart-python/Dockerfile:

```
# Environment Variables
ENV NAME World
```

Next: [Scale the service](https://tutum.freshdesk.com/support/solutions/articles/5000539706).