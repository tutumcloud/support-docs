The **Deploy to Tutum** button allows developers to deploy stacks with one click in Tutum. The button is intended to be added to `README.md` files in public GitHub repositories, although it can be used anywhere else.

This is an example button to deploy our [python quickstart](https://github.com/tutumcloud/quickstart-python):

[![Deploy to Tutum](https://s.tutum.co/deploy-to-tutum.svg)](https://dashboard.tutum.co/stack/deploy/?repo=https://github.com/tutumcloud/quickstart-python)

The button redirects the user to the **Launch new Stack** wizard, with the stack definition already filled with the contents of any of the following files (which will be fetched in the order shown) from the repository (taking into account branch and relative path):

* `tutum.yml`
* `docker-compose.yml`
* `fig.yml`

The user can still modify the stack definition before deployment.


## Adding the 'Deploy to Tutum' button in GitHub

You can simply add the following snipet to your `README.md` file:

	[![Deploy to Tutum](https://s.tutum.co/deploy-to-tutum.svg)](https://dashboard.tutum.co/stack/deploy/)

Tutum will detect the HTTP referer header and deploy the stack file found in the repository, branch and relative path where the source `README.md` file is stored.


## Adding the 'Deploy to Tutum' button in DockerHub

If the button is displayed on the DockerHub, Tutum cannot automatically detect the source GitHub repository, branch and path. In this case, edit the repository description and add the following code:

	[![Deploy to Tutum](https://s.tutum.co/deploy-to-tutum.svg)](https://dashboard.tutum.co/stack/deploy/?repo=<repo_url>)

where `<repo_url>` is the path to your GitHub repository (see below).


## Adding the 'Deploy to Tutum' button anywhere else

If you want to use the button somewhere else (i.e. from external documentation, or a landing site), you just need to create a link to the following URL:

	https://dashboard.tutum.co/stack/deploy/?repo=<repo_url>
	
where `<repo_url>` is the path to your GitHub repository. For example:

* `https://github.com/tutumcloud/quickstart-python`
* `https://github.com/tutumcloud/quickstart-python/tree/staging` to use branch `staging` instead of the default branch
* `https://github.com/tutumcloud/quickstart-python/tree/master/example` to use branch `master` and the relative path `/example` inside the repository

You can use your own image for the link (or no image). Our **Deploy to Tutum** image is available at the following URLs:

* `https://s.tutum.co/deploy-to-tutum.svg`
* `https://s.tutum.co/deploy-to-tutum.png`


