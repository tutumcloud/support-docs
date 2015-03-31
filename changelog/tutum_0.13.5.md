# Tutum 0.13.5

## Added 

- **Create, view, download, and modify a stackfile YAML in Web UI:** it is now possible to interact with the YML definition of a stackfile right from within the Tutum Web UI. No need to upload a new file to edit your stack or guess what the YAML definition looks like for any of your existing stacks.

  ![](http://s.tutum.co.s3.amazonaws.com/support/images/stack-yml-view.png) 

- **Stack file validation:** we've spent some quality time enhancing the validation for stacks. If your stack file YML definition is not valid, you'll now receive meaningful error messages to help you troubleshoot any issues.
 
  ![](http://s.tutum.co.s3.amazonaws.com/support/images/stack-error-messages.png)

- **Service endpoints:** you can now see a list of all the endpoints that your service is publishing in the Web UI. This includes container specific endpoints (e.g. container-1.username.cont.tutum.io) and service endpoints (e.g. service.username.svc.tutum.io).

  ![](http://s.tutum.co.s3.amazonaws.com/support/images/service-endpoints-ui.png)

## Changed

- **Tutum-optimized AWS AMI:** new custom-built tutum-optimized AMI for Amazon Web Services resulting in a tangible speed up when deploying nodes to AWS. New AWS node deployments will automatically use the new AMI. 

## Fixed

- **tutum-agent:** resolved a bug in tutum-agent when installing the agent in a node that was already running docker. 
  
- **Wait for network:** there were some corner cases in some cloud providers where deploying a new node would fail if provisioning took place before the network was ready. To minimize related issues, Tutum will now wait for the network to be ready for all cloud providers.