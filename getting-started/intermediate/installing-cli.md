## Overview

Tutum has a Command Line Interface (CLI) Tool that you can use to interact with the service.

## Install

These are the instructions to install and use the Tutum CLI.

### Linux & Windows

Open your Terminal application and execute the following command:

```
$ pip install tutum
```

<span style="">Check that it has installed correctly:</span>

```
$ tutum -v 
tutum 0.21.0 
```

### Mac OS X

The recommended installation for OS X is using Homebrew. If you don't have brew installed, you can do so here: [http://brew.sh](http://brew.sh)

With Homebrew installed:

```
$ brew install tutum 
```

<span style="">Check that it has installed correctly:</span>

```
$ tutum -v 
tutum 0.21.0
```

## Getting Started

<span style="">First thing is to login, to do so, exectute the following:</span>

```
$ tutum login 
Username: user 
Password: 
Login succeeded! 
```

<span style="">Please visit our</span> [Developer documentation](https://docs.tutum.co/v2/api/) <span style="">site for more information on the CLI.</span>

## Upgrade

### Linux & Windows

```
$ pip install tutum --upgrade
```

### Mac OS X

```
$ brew update && brew upgrade tutum 
```

## Uninstall

### Linux & Windows

Open your Terminal application and execute the following command:

```
$ pip uninstall tutum 
```

### Mac OS X

<span style="">Open your Terminal application and execute the following command:</span>

```
$ brew uninstall tutum 
```