Tutum offers a private registry to its users. This short tutorial will
guide you through the process to upload/push your Docker images to
Tutum’s private registry. 

Application images pushed to Tutum’s private registry will automatically
be shown in the **Tutum Registry** tab section of the **Launch new
service** wizard.

First thing you’ll need to have Docker installed in order to push an
image to Tutum’s registry. Please follow the [official installation
instructions](http://docs.docker.com/installation/) depending on your
system.

With Docker installed:

``` 
$ docker login tutum.co 
Username: user 
Password: 
Email: user@email.com 
Login Succeeded 
$ docker tag my_image tutum.co/user/my_image 
$ docker push tutum.co/user/my_image 
```

Note: In the instructions above, please substitute `user` with your Tutum username, `my_image` with your image’s name, and`user@email.com` with the email you used to register at Tutum.

If you created your account logging in via Docker.com or GitHub, you
will need to [set a password](https://dashboard.tutum.co/account/) before being able to push to the registry.

After you complete those steps, you’ll see that your application image is available for selection under the **Tutum Registry** tab inside the **Private** tab in the **Launch new service** wizard. See [Deploying a private image from Tutum’s private
registry](http://support.tutum.co/support/solutions/articles/5000012154-deploy-your-first) for more details.

**Using the tutum CLI**[](https://docs.tutum.co/features/registry/#using-the-tutum-cli "Permalink to this headline") 

You can also push a local image to Tutum’s private registry using the
CLI. Following the above example:

```
$ tutum login 
Username: user 
Password: 
Login Succeeded 
$ tutum image push my_image 
Pushing my_image to Tutum private registry ... 
Tagging my_image as tutum.co/user/my_image ... 
The push refers to a repository [tutum.co/user/my_image] (len: 1) 
Sending image list 
Pushing repository tutum.co/user/my_image (1 tags) 
Image 511136ea3c5a already pushed, skipping [...] 
Pushing tag for rev [0c292a6f613e] on {https://tutum.co/v1/repositories/user/my_image/tags/latest} 
```

Shortly after the push finishes, the image will appear under the **Tutum
Registry** tab inside the **Private** tab in the **Launch new
service** wizard.
