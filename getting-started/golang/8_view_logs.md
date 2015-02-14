## View logs

Tutum grants you access to the logs your application writes to stdout. A service will multiplex all the logs from all the containers of a service into a single stream of logs. Below you can see the logs for both *web-1* and *web-2*. To see a service's logs:

```
$ tutum service logs web
[web-1] 2015-02-13T23:17:41.054594909Z Listening on port 80 for requests...
[web-1] 2015-02-13T23:18:58.160642022Z web-1 handled HTTP REQUEST at 2015-02-13 23:18:58.160107741 +0000 UTC
[web-1] 2015-02-13T23:18:58.160642022Z MongoDB Status: Not available
[web-2] 2015-02-13T23:24:31.103330213Z Listening on port 80 for requests...
[web-1] 2015-02-13T23:26:43.812500783Z web-1 handled HTTP REQUEST at 2015-02-13 23:26:43.812401474 +0000 UTC
[web-1] 2015-02-13T23:26:43.812500783Z MongoDB Status: Not available
[web-2] 2015-02-13T23:27:00.426419832Z web-2 handled HTTP REQUEST at 2015-02-13 23:27:00.425784882 +0000 UTC
[web-2] 2015-02-13T23:27:00.426419832Z MongoDB Status: Not available
```

To see a specific container's logs:

```
$ tutum container logs web-1
2015-02-13T23:17:41.054594909Z Listening on port 80 for requests...
2015-02-13T23:18:58.160642022Z web-1 handled HTTP REQUEST at 2015-02-13 23:18:58.160107741 +0000 UTC
2015-02-13T23:18:58.160642022Z MongoDB Status: Not available
2015-02-13T23:26:43.812500783Z web-1 handled HTTP REQUEST at 2015-02-13 23:26:43.812401474 +0000 UTC
2015-02-13T23:26:43.812500783Z MongoDB Status: Not available
```

Visit your application in the browser (or using curl) again, print the logs to screen again, and you’ll see another log message generated.

Next: [Load balance the service](https://tutum.freshdesk.com/support/solutions/articles/5000559797).