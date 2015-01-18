## Set up

In this step you will install the Tutum CLI. This provides you access to the Tutum Command Line Interface tool.

**Linux**

Open your Terminal application and execute the following command:

```
$ pip install tutum
```

**Mac**

The recommended installation for OS X is using Homebrew. If you don't have brew installed, you can learn how to here: [http://brew.sh](http://brew.sh) or paste the following command at a terminal prompt.

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

With Homebrew installed:

```
$ brew install tutum
```

**Check Tutum CLI is installed**

Check that it has installed correctly:

```
$ tutum -v
0.11.2
```
Once installed you can use the `tutum` command from your command shell.

Log in using the username and pasword you used when creating your Tutum account:

**Login**

```
$ tutum login
Username: python-user
Password:
Login succeeded!
```

Authenticating is required to proceed with this tutorial.

In order to be able to simply copy and paste some of the commands in the next sections of this tutorial, your Tutum username needs to be available as an environment variable in your system. 

You do this by executing the following in the terminal prompt (change `python-user` to your username):

```
$ export TUTUM_USER=python-user
```
Find the documentation for the Tutum CLI tool and API [here](https://docs.tutum.co/v2/api/?shell).

Next: [Prepare the app](https://tutum.freshdesk.com/support/solutions/articles/5000539696).
