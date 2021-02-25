# API Gateway
 
APIs are a way for software to talk to other software. Used extensively
within software development industry, and usually run 24/7 365 days a year.

To over simplify API, they exchange information to attempt to perform an action.

## Types

There are different types such as REST and WebSocket based APIs. 

The AWS API Gateway service is regional, but you can also use edge locations. Can be pprovisioned into VPCs to make them private for internal.

REST - request and response
WebSocket - real time dashboards, alerting, config
can be used to add interactivity between the clients

## Good to Know Facts

* you can version the API using stages
* provides a mock/test integration to provide a static response so that you can
  test before the backend service is ready to hook up to it.
* can be setup to trigger Lambda functions, for event driven architecture???
* Can cache individual APIs???
* Can be protected/filtered with WAF/Web ACL.
* Can integrate with Cloudwatch and XRay for logs and tracing.
* read/write to support direct integrations???