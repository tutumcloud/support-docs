Tutum can automatically test your GitHub repositories using containers. For this, you will need to specify a `docker-compose.test.yml` file in the root of your repository which defines a `sut` service with the test to be run.

For example:

```
sut:
  build: .
  command: run_tests.sh
```

This will build the repository and run the `run_tests.sh` file inside a container using the built image.

You can define any number of linked services in this file. The only requirement is that `sut` is defined. Its return code will be used to decide if tests passed or not: tests will **pass** if the `sut` service returns `0`, or will **fail** otherwise.


## Enabling automated tests on a repository

To enable testing on a GitHub repository, you must first create a repository in Tutum associated with it. [Learn more](https://support.tutum.co/support/solutions/articles/5000638474)

By default, every automated build will run any defined tests prior to push. Optionally, you can enable the **automated tests** setting on the repository, which will force test runs for all commits pushed to GitHub, and optionally for all pull requests opened against the source repository as well. The following options are available:

* `Off`: only commits to branches that have autobuild configured will be tested
* `Source Repository`: commits to all branches of the source GitHub repository will be automatically tested, regardless of their autobuild setting
* `Source Repository & External Pull Requests`: commits to all branches of the source GitHub repository will be automatically tested, as well as any pull requests opened against it


## Checking your test results

In the repository view, click on **Timeline**. You will be able to see the pending, in progress, successful and failed builds and test runs for the repository. You can check the logs of each test run by clicking to expand the timeline entry.


## Advanced options

Testing is performed using our open source [tutum/builder](https://github.com/tutumcloud/builder) image. The following options are available to customize your tests:


### Available environment variables for testing

The following environment variables are available when executing the `docker-compose.test.yml` file:

* `GIT_BRANCH` which contains the name of the branch that is currently being tested
* `GIT_TAG` which contains the commmit hash being tested
* `IMAGE_NAME` which contains the name of the docker repository being built (not defined for automated tests triggered outside of an automated build)

You can use the above environment variables by setting them in your `sut` service:

```
sut:
  build: .
  command: run_tests.sh
  environment:
    - GIT_BRANCH
```


### Using private repositories in your tests

If you use a private repository, you have to add it to your repositories with appropiate credentials first. Tutum will inject the appropiate docker credentials to the build container in order to pull private repositories as part of your tests.


### Multiple docker-compose test files

You can define more than one `docker-compose.test.yml` files if you need to: any file that ends in `.test.yml` will be used for testing. Tests will run sequentially.


### Custom hooks

If you need to run custom commands between phases of the build process, you can define hooks. The following hooks are available:

* `hooks/post_checkout`
* `hooks/pre_build`
* `hooks/post_build`
* `hooks/pre_test`
* `hooks/post_test`
* `hooks/pre_push`
* `hooks/post_push`

Create a file in your code repository in a folder called hooks with those names and the builder will execute them before and after each step.

