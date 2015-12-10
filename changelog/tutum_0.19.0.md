# Tutum 0.19.0

## Added

- **Secure API keys:** Tutum now supports multiple API keys per account. To enhance security, these new keys are automatically hashed after creation. Existing API keys will be migrated and will continue to work. API keys should now be used as passwords with the API via Basic authentication - the current "ApiKey" authentication header is now deprecated. [See docs](https://docs.tutum.co/v2/api/#authentication)

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.19.0/secure-keys.png)

- **Build Environment Variables:** you can now define specific environment variables to be used for Docker repository builds and tests. This can be very useful if your builds and/or tests need to access third party services and require tokens for authentication. You can add these environment variables from the Repository edit view.

  ![](http://s.tutum.co.s3.amazonaws.com/changelog/0.19.0/Build_env_vars.png)

- **Support for external v2-only Docker registries:** you can now use external registries in Tutum that are only compatible with version 2 of the Docker registry API.

## Changed/Updated

- **Tutum CLI:** new and shiny version 0.21.0 available. **Please note** that CLI versions older than 0.20.2 are not compatible with the new *Secure API Keys*, please make sure to update the CLI; failure to do so may prevent you from logging and/or interacting with Tutum using the CLI.

- **Overlay network:** we've updated our overlay network to [weave 1.3.1](https://github.com/weaveworks/weave/blob/master/CHANGELOG.md#release-131)

## Fixed

- Fixed a bug that prevented you from editing a service when the image tag no longer existed. Thanks to everyone that pointed out this issue!

- More than 100 minor fixes and improvements in performance, stability and security as we ready up for GA in Q1 2016! Tip: it's time to start getting excited :)
