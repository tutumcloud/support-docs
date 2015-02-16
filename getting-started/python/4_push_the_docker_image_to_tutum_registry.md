## Push the Docker image to Tutum's Registry

*Skip this step if you don't have Docker installed locally.*

In this step you will push the resulting image from the step before to Tutum's private registry. 

```
$ tutum image push quickstart-python
Pushing quickstart-python to Tutum private registry ...
Tagging quickstart-python as tutum.co/python-user/quickstart-python ...
Sending image list
Pushing repository tutum.co/python-user/quickstart-python (1 tags)
Image 511136ea3c5a already pushed, skipping
Image 16386e29a1f4 already pushed, skipping
Image 835c4d274060 already pushed, skipping
Image fa0476ea9115 already pushed, skipping
Image c8e506fcb72c already pushed, skipping
Image 46c3f54a0542 already pushed, skipping
Image 257a71bccbe6 already pushed, skipping
Image d743a8dce772 already pushed, skipping
Image 0ed2c918ccb9 already pushed, skipping
Image f3a75e6be420 already pushed, skipping
Image 4f3dd1fe9cea already pushed, skipping
Image 37fd289d419e already pushed, skipping
203a97de5067: Image successfully pushed
409b52643404: Image successfully pushed
f32b97a40886: Image successfully pushed
11ceaff64fab: Image successfully pushed
a982e923e161: Image successfully pushed
Pushing tag for rev [a982e923e161] on {https://tutum.co/v1/repositories/python-user/quickstart-python/tags/latest}
```

After the image is pushed successfully, you can verify that the image is now in Tutum's registry by executing:

```
$ tutum image list
NAME                                    DESCRIPTION
tutum.co/python-user/quickstart-python
```

Next: [Deploy the app as a Tutum service](https://support.tutum.co/support/solutions/articles/5000539698).