Tutum can automatically build images from GitHub repositories. To enable this, you must follow these steps:

1. Link your GitHub account
2. Create an empty repository in Tutum's registry
3. Edit the repository to configure the source GitHub repository and the source branches for each repository tag to be built

Once your repository is configured, a _git push_ to a branch which has been set as a tag source will trigger a build.

Builds are done inside containers which run on your nodes. They will be deployed using an "emptiest node" strategy. If you want to force the build on a specific subset of nodes, you can add a node tag `builder` to them.

You can still push to these repositories even if they have been configured to be automatically built.

After build and before pushing the image, tests will be run if configured. [Learn more about image testing](https://support.tutum.co/support/solutions/articles/5000638476)


## Link your GitHub account

Click on your avatar on the top right corner, and select **Account info**. Select **Source Providers** from the left menu:

![](http://s.tutum.co/support/images/source-providers.png)

Click on **Link account** to start the authorization flow with GitHub. Click on **Authorize application** when asked, and your account is linked!


## Creating an empty repository on Tutum's registry

Go to the **Repositories** section on the top menu, then click on **Create your first repository**:

![](http://s.tutum.co/support/images/create-repository.png)

Enter a **name** and an optional **description**, and click on **Create**.

Once created, you can either push to it manually using docker's or Tutum's CLI, or configure automated builds.

## Adding a repository from a third party registry

If you want to automatically build a repository which is hosted in Docker Hub or in another third party registry, click on the **Add from third party registry**:

![](http://s.tutum.co/support/images/third-party-images-modal.png)

Enter the repository name that you want to add. For example:

* `username/reponame` for repositories hosted in the Docker Hub
* `registry.com/namespace/reponame` for repositories hosted in other third party registries, where `registry.com` is the hostname of the registry

You must also provide credentials with **push** permission. Providing **read-only** credentials will allow you to deploy the repository but not to automatically build it.


## Configuring automated build settings

From the repository view, click on **Edit**:

![](http://s.tutum.co/support/images/edit-repository.png)

Select the source **GitHub repository** to be used for building the repository, and then add one or more tags to be built. Each tag needs a source branch and optionally a path to the Dockerfile relative to the GitHub repository root.

Click on **Save**. A webhook will automatically be added to your GitHub repository for Tutum to get notified on every push. A push to a branch used as the source for one or more tags will trigger a build.


## Checking your active builds

In the repository view, click on **Timeline**. You will be able to see the pending, in progress, successful and failed builds for any tag of the repository. You can check the logs of each build by clicking to expand the timeline entry.

You can cancel pending builds and builds that are being executed by clicking on the **Cancel** button:

![](http://s.tutum.co/support/images/cancel-build.png)


## Autoredeploy services on successful build

After a build has been successful, you can configure your services to automatically redeploy with the new version. [Learn more about autoredeploy](https://support.tutum.co/support/solutions/articles/5000569896)

## Adding automated tests

If you want to test your code before the image is built and pushed, you can use Tutum's [automated testing](https://support.tutum.co/support/solutions/articles/5000638476) feature which integrates seamlessly with the above workflow.


## Under the hood

Automated builds are powered by our open source [tutum/builder](https://github.com/tutumcloud/builder) image. You can use this image yourself to do local builds or tests.
