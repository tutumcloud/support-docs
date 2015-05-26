# Tutum 0.15.0

## Added 

- **Support for `docker exec` in Tutum CLI and Web UI.** Run a command in a running container. When using the CLI you can choose which command to run. In the Web UI, the commands default to `sh` which gives users a shell in their browsers.
 
  ![](http://s.tutum.co/changelog/0.15.0/docker-exec-ui.gif)
  
- **Colored Service Logs**. It is now easier than ever to tell containers apart in your service logs! Every container is uniquely identified with its own color.

  ![](http://s.tutum.co/changelog/0.15.0/colored_logs.gif)

- **Email Notifications.** Get notified when something fails or every time something happens. [Activate here](https://dashboard.tutum.co/account/#container-notifications)

  ![](http://s.tutum.co/changelog/0.15.0/email.png)

- **Slack Notifications.** Get notified when something fails or every time something happens - integrated natively into [Slack](http://slack.com). Because [Tutum <3 Slack](https://tutum-community.slack.com/). [Learn more](https://support.tutum.co/support/solutions/articles/5000626929)

  ![](http://s.tutum.co/changelog/0.15.0/slack.png)

- **Stream API for container and service logs.** What's even better than accessing your logs over a RESTful API? Accessing them over a Stream API! No more pulling - get logs pushed your way with the new Stream API. [Learn more](https://docs.tutum.co/v2/api/?shell#get-the-logs-of-a-container)
 
- **Tutum CLI now supports `--follow` and `--tail` for logs.** It has been implemented using the new *Stream API* for container and service logs. `--follow` is disabled by default; when active, it will follow the log output as new logs are received. `--tail` lets you specify the number of lines to show from the end of the logs, with a default value of `--tail=all`. [Learn more](https://github.com/tutumcloud/tutum-cli)

- **Official support for CentOS** [Learn more](http://blog.tutum.co/2015/05/25/tutum-now-supports-centos/)

  ![](http://s.tutum.co/changelog/0.15.0/tutum%20support%20centos.png)

## Changed
- **Upgraded Weave to version 0.10.0**

- **Changed `autorestart` to `restart` in Stackfiles.** This change enables backwards compatibility with your existing `docker-compose.yml` files. [Learn more](https://docs.tutum.co/v2/api/?shell#stacks)

- **Deprecated REST API for container and service logs.** Please update your applications to make use of the new and improved Stream API. [Learn more](http://docs.tutum.co/v2/api/?shell#stream-api)

## Fixed
- **Fixed timeouts when loading repositories/images with many tags.**

- **Fixed timeouts when creating stacks with many services.**

- **Fixed `--autoredeploy` flag in CLI to match API.**
