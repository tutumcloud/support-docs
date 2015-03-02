A **stack** is a collection of services that make up an application in a specific environment. A **stack file** is a file in YAML format that define one or more services.

A stack is a convenient way to automate the deployment of multiple services that are linked to each other, without the need to define one by one.

As stack files also define environment variables, deployment tags, number of containers and related environment-specific configuration, it is recommended to use one stack file per environment (dev, test, prod...).

## Creating a stack

### Using the web interface

Go to the **Stack** section, and click on **Create a stack**. In the wizard, provide a name to the stack and select a stack file from your computer (by clicking on the field or by dragging the file to the field directly). Then, click on **Create and deploy**.

![](https://s.tutum.co/support/images/create-stack-wizard.png)

### Using the API

You can also create a new stack by uploading it directly to our API. Please note that in this case, the stack file has to be in **JSON** format, like the following example:

```
POST /api/v1/stack/ HTTP/1.1
{
	"name": "my-new-stack",
	"services": [
		{
			"name": "hello-word",
			"image": "tutum/hello-world",
			"target_num_containers": 2
		}
	]
}
```

Check our [API documentation](https://docs.tutum.co/v2/api/?http#stacks) for more information.

### Using the CLI

You can create a stack from a YAML file by executing:

```
tutum stack create -f tutum.yml
```

Check our [CLI documentation](https://docs.tutum.co/v2/api/?shell#stacks) for more information.


## Update an existing stack

### Using the web interface

On the stack detail view, click on **Edit**. Select a stack file from your computer (by clicking on the field or by dragging the file to the field directly). Then, click on **Save**.

### Using the API

You can also update a stack by uploading the new file directly to our API. Please note that in this case, the stack file has to be in **JSON** format, like the following example:

```
PATCH /api/v1/stack/(uuid)/ HTTP/1.1
{
	"services": [
		{
			"name": "hello-word",
			"image": "tutum/hello-world",
			"target_num_containers": 2
		}
	]
}
```

Check our [API documentation](https://docs.tutum.co/v2/api/?http#stacks) for more information.

### Using the CLI

You can update a stack from a YAML file by executing:

```
tutum stack update -f tutum.yml (uuid or name)
```

Check our [CLI documentation](https://docs.tutum.co/v2/api/?shell#stacks) for more information.
