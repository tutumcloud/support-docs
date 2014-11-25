## Why is Tutum not production-ready and in beta?

The features that Tutum offers today, and that will continue to be developed and made available, are sufficiently stable to be considered production-ready. However, not all the features we believe to be enough for Tutum to satisfy the use cases it aims to satisfy are available today. It is for this reason that Tutum remains in *beta status*.

## Breaking changes, what to expect:

We are committed to minimizing the number of breaking changes as we introduce new features, but since Tutum is still actively being developed, we cannot guarantee there will not be any breaking changes in the API, CLI, libraries until we come out of *beta*.

## When will Tutum exit beta status and be production ready?

Planning for this to happen early Q2 2015. 

## What are some key features/functionality missing from Tutum for it to come out of beta?

**Support for volumes:** the ability for data to persist beyond the lifetime of a container, and for the data to be shared by multiple containers.

**Support for templates/manifests for stacks (a group of services):** the ability to define a set of services, their links, environment variables, volumes, etc. in a structured file format (ie. YAML) and have Tutum deploy directly from said definition. This is akin to Fig's fig.yml, with which we'll attempt for Tutum to be compatible with. 

**Suppor for build and push:** the ability to build from Dockerfile, git (including public/private Github and Bitbucket repositories) or tarball and subsequent push of the resulting image to any pubilc or private Docker registry (ie. DockerHub, Tutum Registry, Quay.io)

**Support for BYOH (bring your own host):** the ability to install the *tutum agent* on any Linux host that is accesible via the Internet to be used as a container endpoint by Tutum. This means users will no longer be required to provide Tutum with access to their cloud infrastructures. 

## Is anyone using Tutum for production-level deployments?

Yes, if your application does not require any of the missing features, like volumes, there should not be any impediments for you to use Tutum to deploy your app.

## What happens to my running applications if Tutum crashes, goes down or becomes unavailable?

Because of how Tutum works, if Tutum were to become unresponsive or unavailable, your applications will remain unaffected and continue to work without any problems.

This is because your applications get deployed to your own infrastructure, not Tutum's. As long as your infrastructure is available, even if Tutum is not, your applications will continue to work. 

Having said this, since Tutum was made available in September 2014, we have yet to experience any unexpected downtime.
