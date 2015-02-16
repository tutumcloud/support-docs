##Prepare the app

In this step, you will prepare a simple application that can be deployed. Execute the following command to clone the sample application:

```
$ git clone https://github.com/tutumcloud/quickstart-go.git
$ cd quickstart-go
```
*Skip the following step if you don't have Docker installed locally*

Next, we have to build this application. Execute the following command to build the app. This will create a Docker image and tag it as "quickstart-go": 

```
$ tutum build --tag quickstart-go .
```

Next: [Push the Docker image to Tutum's Registry](https://support.tutum.co/support/solutions/articles/5000559792).