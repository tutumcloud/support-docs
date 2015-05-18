# SSHing into a Tutum-managed node

The recommended way to get SSH access to Tutum-provisioned nodes is using a container to update the *authorized_keys* file in the node(s) with a public SSH key. 

This is the suggested image to do this: 

### tutum/authorizedkeys

Container image to copy SSH public key to the host's /.ssh/authorized_keys file

- Github: [https://github.com/tutumcloud/authorizedkeys](https://github.com/tutumcloud/authorizedkeys).
- DockerHub: [http://hub.docker.com/u/tutum/authorizedkeys](http://hub.docker.com/u/tutum/authorizedkeys)


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
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC4PHh4WJqUgiWedmkIJS+L1IwxfXHkfYC0N9NZ28quXyL4zQq2CDeCQrS0RDESklnuZVCe9p5fjgEHcy+FsiTUaBbjzCndeO++gqAM6pKy4ziEY1JNpIBpbuyVIK6AJIqTWzcqprhw4G8PZetLoHug3BWiiwsIW7WHhNNsrEVEsTCnCc5vG97IHZ0A6TlP6HGvVSfCFPZiAxP48hsoEsEGjcCvY9tgJa4k60XWtHbPWtjOi90RFt9OKcbUsZa+vq/3lBG50XbMoQm3NS6A+UQQ7SKvzmwJSIYCqo5lu9UzQbVKy9o00NqXa5jkmZ9Yd0BJBjFmb3WwUR8sJWZVTPFL
```

### Create a stack in Tutum

Click the button below to create a new Stack in Tutum with the correct configuration.

[![Deploy to Tutum](https://s.tutum.co/deploy-to-tutum.svg)](https://dashboard.tutum.co/stack/deploy/?repo=https://github.com/tutumcloud/authorizedkeys)

The Stackfile is as follows:

```
authorizedkeys:
  image: tutum/authorizedkeys
  deployment_strategy: every_node
  autodestroy: always
  environment:
    - AUTHORIZED_KEYS=ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC4PHh4WJqUgiWedmkIJS+L1IwxfXHkfYC0N9NZ28quXyL4zQq2CDeCQrS0RDESklnuZVCe9p5fjgEHcy+FsiTUaBbjzCndeO++gqAM6pKy4ziEY1JNpIBpbuyVIK6AJIqTWzcqprhw4G8PZetLoHug3BWiiwsIW7WHhNNsrEVEsTCnCc5vG97IHZ0A6TlP6HGvVSfCFPZiAxP48hsoEsEGjcCvY9tgJa4k60XWtHbPWtjOi90RFt9OKcbUsZa+vq/3lBG50XbMoQm3NS6A+UQQ7SKvzmwJSIYCqo5lu9UzQbVKy9o00NqXa5jkmZ9Yd0BJBjFmb3WwUR8sJWZVTPFL
  volumes:
    - /root:/user:rw
```

Make sure to change the AUTHORIZED_KEYS with the public key you copied to your clipboard in the previous step. 

Click on **Create and deploy**

*Note: the default configuration will copy the public key above to ALL of your existing nodes.*

### SSH into Tutum node

Get the node IP from Tutum:

![](http://cl.ly/image/2t373J2i2f1b/Screen%20Shot%202015-02-02%20at%2023.29.02.png)

SSH to the node as `root`:

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
