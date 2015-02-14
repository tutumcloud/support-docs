## Define environment variables

Docker lets you externalize configuration - storing data such as encryption keys or external resource addresses in environment variables. Tutum makes it easy to define, share, and update the environment variables of your services.

At runtime, environment variables are exposed to the application inside the container.

Open the file in *quickstart-go/main.go*, and take a look at the *fmt.Fprintf* call in the *indexHandler* method:

```
fmt.Fprintf(w, "<h1>hello, %s</h1>\n<b>Hostname: </b>%s<br><b>MongoDB Status: </b>%s", os.Getenv("NAME"), hostname, mongostatus)
```

You'll see that the code uses **os.Getenv("NAME")** to get the environment variable **NAME**. If you modify the enviroment variable, the message should change accordingly. Try that by executing:

```
$ tutum service set --env NAME="Golang users" --redeploy web
```

Execute `$ tutum container ps --service web` again to get the new container endpoint. You'll see that there are now two `web-1` containers, one with a status of **terminated** and another one **starting** or **running**.

```
$ tutum container ps --service web
NAME    UUID      STATUS        IMAGE                                      RUN COMMAND      EXIT CODE  DEPLOYED        PORTS
web-1   01777963  ✘ Terminated  tutum.co/borjaburgos/quickstart-go:latest                          -1  23 minutes ago  web-1.borjaburgos.cont.tutum.io:49162->80/tcp
web-1   1fe3a0a2  ▶ Running     tutum.co/borjaburgos/quickstart-go:latest                              2 seconds ago   web-1.borjaburgos.cont.tutum.io:49176->80/tcp
```
Now curl the new endpoint to see the updated *hello, Golang users* greeting. *Note: if you don't see an endpoint, wait until the container status changes to **running**.*

    $ curl web-1.$TUTUM_USER.cont.tutum.io:49176
    <h1>hello, Golang users</h1>    
    <b>Hostname: </b>web-1<br><b>MongoDB Status: </b>Not available%

Your service now returns `hello, Golang users`, good job on modifiying your service using environment variables!

### Environment Variables and the Dockerfile

Environment variables can be set in the Dockerfile, and modified at runtime (as you just did). 

If you are wondering where the default value for the **NAME** environment variable is set, checkout the file *quickstart-go/Dockerfile*:

```
ENV NAME world
```

Next: [Scale the service](https://tutum.freshdesk.com/support/solutions/articles/5000559795).