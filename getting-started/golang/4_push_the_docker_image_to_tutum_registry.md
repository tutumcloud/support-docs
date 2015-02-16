## Push the Docker image to Tutum's Registry

*Skip this step if you don't have Docker installed locally.*

In this step you will push the resulting image from the step before to Tutum's private registry. 

```
$ tutum image push quickstart-go
Pushing quickstart-go to Tutum private registry ...
Tagging quickstart-go as tutum.co/golang-user/quickstart-go ...
Sending image list
Pushing repository tutum.co/borjaburgos/quickstart-go (1 tags)
Image 511136ea3c5a already pushed, skipping
Image 8771fbfe935c already pushed, skipping
Image 0e30e84e9513 already pushed, skipping
Image c90a56bfe7dd already pushed, skipping
Image 6b030fdd4748 already pushed, skipping
Image 5b691e49c664 already pushed, skipping
Image 1ea09c2dbbab already pushed, skipping
Image d560761777e0 already pushed, skipping
Image 6c9ce5fcafa4 already pushed, skipping
Image fdaf64c52e5d already pushed, skipping
Image d6429349e0af already pushed, skipping
Image b77e2c7c5469 already pushed, skipping
Image 4fb0e42c842e already pushed, skipping
Image 2fb1c97e2c4f already pushed, skipping
Image 7b9d831c9cf1 already pushed, skipping
7b9ee289fc2e: Image successfully pushed
9863bcbb7867: Image successfully pushed
54e942054d03: Image successfully pushed
54411cc6888d: Image successfully pushed
ba323265f1d3: Image successfully pushed
Pushing tag for rev [a982e923e161] on {https://tutum.co/v1/repositories/golang-user/quickstart-go/tags/latest}
```
After the image is pushed successfully, you can verify that the image is now in Tutum's registry by executing:

```
$ tutum image list
NAME                                    DESCRIPTION
tutum.co/golang-user/quickstart-go
```

Next: [Deploy the app as a Tutum service](https://support.tutum.co/support/solutions/articles/5000559793).