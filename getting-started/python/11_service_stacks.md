## Service Stacks

### Introduction

A stack is a logical grouping of related services that are usually deployed together and require each other to work as intended. If you are familiar with *fig* or *Docker Compose* then you should feel right at home with *Tutum Service Stacks*. 

The three services that you created earlier form a stack with 3 layers: the load-balancing layer, the application layer and the data layer. The definition of a stack is kept in a Stackfile. Checkout the file /quickstart-python/Stackfile.yml for a Stackfile defining the 3 services (lb, web, redis) you created in the previous steps. 

This is what a Stackfile looks like:

```
STACKFILE
```

### Running a stack

Running a stack only requires one command to be executed in the path containing your Stackfile.yml:

```
$ tutum up
```

Alternatively, you can specify the YML file to use and its location:

```
$ tutum up /usr/tutum/quickstart-python/Stackfile.yml
```

You can read more information about Stacks and Stackfiles [here]().