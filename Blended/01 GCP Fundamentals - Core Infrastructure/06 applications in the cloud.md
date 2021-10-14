# App Engine

## Standard 
* usage based pricing
* free daily quota
* can test locally via SDK
* runtime environments
  * Java
  * Python
  * PHP
  * Go
* sandbox
  * no writing to local files
  * all requests time out at 60s
  * limits on 3rd party software
  * 

## Flexible
* no sandbox
* use containers
* update OS versions automatically

## Comparison

| | Standard | Flexible |
| --- | --- | --- |
| startup | milliseconds | minutes |
| SSH | no | yes (not default) |
| write to disk | no | ephemeral |
| 3rd party binaries | no | yes |
| network access | only via services | yes |
| free, then per-instance class | provisioned | 

* App Engine Flexible vs GKE?
  * App engine - you have app and want Google to deploy/manage
  * GKE - have your won infrastructure

# API Management

## Cloud Endpoints
* control access and validate through JWT
* identify users through Auth0 & Firebase
* monitor & log use
* generate client libs (?)
* supports
  * app engine flex
  * GKE
  * GCE

## Apigee Edge
* focus on business problems
