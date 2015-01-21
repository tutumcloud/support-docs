## View logs

Tutum grants you access to the logs your application writes to stdout. A service will multiplex all the logs from all the containers of a service into a single stream of logs. Below you can see the logs for both *web-1* and *web-2*. To see a service's logs:

```
$ tutum service logs web
[web-1] 2015-01-13T22:45:37.250431077Z  * Running on http://0.0.0.0:80/
[web-1] 2015-01-07T17:20:19.076174813Z 83.50.33.64 - - [07/Jan/2015 17:20:19] "GET / HTTP/1.1" 200 -
[web-1] 2015-01-07T17:20:34.209098162Z 83.50.33.64 - - [07/Jan/2015 17:20:34] "GET / HTTP/1.1" 200 -
[web-1] 2015-01-07T18:46:07.116759956Z 83.50.33.64 - - [07/Jan/2015 18:46:07] "GET / HTTP/1.1" 200 -
[web-2] 2015-01-07T18:48:24.550419508Z  * Running on http://0.0.0.0:5000/
[web-2] 2015-01-07T18:48:37.116759956Z 83.50.33.64 - - [07/Jan/2015 18:48:37] "GET / HTTP/1.1" 200 -
```

To see a specific container's logs:

```
$ tutum container logs web-1
2015-01-07T17:18:24.550419508Z  * Running on http://0.0.0.0:80/
2015-01-07T17:20:19.076174813Z 83.50.33.64 - - [07/Jan/2015 17:20:19] "GET / HTTP/1.1" 200 -
2015-01-07T17:20:34.209098162Z 83.50.33.64 - - [07/Jan/2015 17:20:34] "GET / HTTP/1.1" 200 -
2015-01-07T18:46:07.116759956Z 83.50.33.64 - - [07/Jan/2015 18:46:07] "GET / HTTP/1.1" 200 -
```

Visit your application in the browser (or using curl) again, print the logs to screen again, and you’ll see another log message generated.

Next: [Load balance the service](https://tutum.freshdesk.com/support/solutions/articles/5000539709).