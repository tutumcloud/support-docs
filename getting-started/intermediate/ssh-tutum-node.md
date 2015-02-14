# SSHing into a Tutum-managed node

Currently Tutum uses a private key to provision nodes to IaaS providers on behalf of the user. Unfortunately, this means that users do not have an easy way to access (SSH) into these nodes.

In the future, Tutum intends for users to have the ability to provide their own public keys, which will then be added to ~/.ssh/authorized_keys as part of the priviosining process. This feature does not exist today. 

The recommended way to get SSH access to Tutum-provisioned nodes is using a container to update the *authorized_keys* file in the node(s).

This is the recommended container image/repository to do this: 

### borja/authkey

Container image to copy SSH public key to the host's /.ssh/authorized_keys file

- Github: [https://github.com/borjaburgos/docker-authkey](https://github.com/borjaburgos/docker-authkeys).
- DockerHub: [http://hub.docker.com/u/borja/authkey](http://hub.docker.com/u/borja/authkey)



## To use in Tutum

### Create pair of keys 

```
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/borjaburgos/.ssh/id_rsa): tutum
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in tutum.
Your public key has been saved in tutum.pub.
The key fingerprint is:
ac:76:05:19:51:fa:3e:f0:c8:80:73:0d:9f:6b:b7:8f borjaburgos@MacBookPro
The key's randomart image is:
+--[ RSA 2048]----+
|        oo.      |
|         +       |
|      . +        |
|     . = +       |
|    o o S o      |
|     o + B       |
|      o * =      |
|     . o . +     |
|          E..    |
+-----------------+
```

Print your public key to the terminal and copy it to your clipboard.

```
$ more tutum.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC4PHh4WJqUgiWedmkIJS+L1IwxfXHkfYC0N9NZ28quXyL4zQq2CDeCQrS0RDESklnuZVCe9p5fjgEHcy+FsiTUaBbjzCndeO++gqAM6pKy4ziEY1JNpIBpbuyVIK6AJIqTWzcqprhw4G8PZetLoHug3BWiiwsIW7WHhNNsrEVEsTCnCc5vG97IHZ0A6TlP6HGvVSfCFPZiAxP48hsoEsEGjcCvY9tgJa4k60XWtHbPWtjOi90RFt9OKcbUsZa+vq/3lBG50XbMoQm3NS6A+UQQ7SKvzmwJSIYCqo5lu9UzQbVKy9o00NqXa5jkmZ9Yd0BJBjFmb3WwUR8sJWZVTPFL borjaburgos@MacBookPro
```

### Create a service in Tutum

Create a new service and search for the image in **Public Images > Search Docker hub**. Search for `borja/authkey`.

To make sure this key makes it to all of your Digital Ocean nodes, for example, select `Deploy tag` as **digitalocean** and `Deployment strategy` as **Every node**. Set Autodestroy to `ON`.

![](http://cl.ly/image/1W1D2d323w1e/download/Screen%20Shot%202015-02-02%20at%2023.19.54.png)

### Environment variables

Paste your clipboard from earlier. Do not add any quotation signs. 

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC4PHh4WJqUgiWedmkIJS+L1IwxfXHkfYC0N9NZ28quXyL4zQq2CDeCQrS0RDESklnuZVCe9p5fjgEHcy+FsiTUaBbjzCndeO++gqAM6pKy4ziEY1JNpIBpbuyVIK6AJIqTWzcqprhw4G8PZetLoHug3BWiiwsIW7WHhNNsrEVEsTCnCc5vG97IHZ0A6TlP6HGvVSfCFPZiAxP48hsoEsEGjcCvY9tgJa4k60XWtHbPWtjOi90RFt9OKcbUsZa+vq/3lBG50XbMoQm3NS6A+UQQ7SKvzmwJSIYCqo5lu9UzQbVKy9o00NqXa5jkmZ9Yd0BJBjFmb3WwUR8sJWZVTPFL borjaburgos@MacBookPro
```

![](http://cl.ly/image/1u3R0W2g1p0E/download/Screen%20Shot%202015-02-02%20at%2023.22.27.png)

### Volumes

Add a volume `/.ssh`:`/root/.ssh`

![](http://cl.ly/image/1A022Z0m1n2t/download/Screen%20Shot%202015-02-03%20at%2015.40.06.png)

Click on **Create and deploy**

### SSH into Tutum node

Get the node IP from Tutum

![](http://cl.ly/image/2t373J2i2f1b/Screen%20Shot%202015-02-02%20at%2023.29.02.png)

```
$ ssh -i ~/tutum root@104.236.69.138
The authenticity of host '104.236.69.138 (104.236.69.138)' can't be established.
RSA key fingerprint is 4b:22:71:39:53:4a:88:51:4b:a7:2e:ed:03:dd:a3:7f.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '104.236.69.138' (RSA) to the list of known hosts.
Welcome to Ubuntu 14.04.1 LTS (GNU/Linux 3.13.0-40-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Mon Feb  2 23:29:53 EST 2015

  System load:  0.2                Users logged in:        0
  Usage of /:   16.0% of 19.56GB   IP address for eth0:    104.236.69.138
  Memory usage: 52%                IP address for eth1:    10.132.224.214
  Swap usage:   0%                 IP address for docker0: 172.17.42.1
  Processes:    111

  Graph this data and manage this system at:
    https://landscape.canonical.com/

Last login: Mon Feb  2 23:29:54 2015 from pool-108-30-19-181.nycmny.fios.verizon.net
root@13e9d739-admin:~#
```
