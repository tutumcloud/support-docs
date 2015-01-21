## Prepare the app

In this step, you will prepare a simple application that can be deployed. Execute the following command to clone the sample application:

```
$ git clone https://github.com/tutumcloud/quickstart-python.git
$ cd quickstart-python
```
*Skip the following step if you don't have Docker installed locally*

Next, we have to build this application. Execute the following command to build the app. This will create a Docker image and tag it as "quickstart-python": 

```
$ tutum build --tag quickstart-python .
```

Next: [Push the Docker image to Tutum's Registry](https://tutum.freshdesk.com/support/solutions/articles/5000539697).