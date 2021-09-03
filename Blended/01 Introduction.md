# What is cloud computing?
* on-demand self-service 
* broad network access
* resource pooling (multi-tenant)
* rapid elasticity
* measured service

# Where are we going?
1. physical / co-located
    * user configured
    * user managed and maintained
2. virtualised
   * user configured
   * provider managed and maintained
3. serverless
   1. fully-automated

# What level of infrastructure 
compute engine - gke - app engine - cloud functions - managed services  
IAAS - hybrid - PAAS - serverless - automated elastic resources  
< managed infrastruture ................................ dynamic infrastructure >

# Geography
Zone - Multi-Region - Region - Zone
* Datacentres vs Edge Point of Presence (different to CDN Point of Presence)

# How to save money
* billing in sub-hour increments
* discounts for sustained use
* discounts for committed use
* discounts for pre-emptible use
* custom VM instance types

# Compute Services
* compute engine
* gke
* app engine
* cloud functions
* cloud run (based on knative)
* 
# Storage Services
* cloud bigtable
* cloud storage
* cloud sql
* 2 more

# Data Handling
* BigQuery etc.

# Billing
* can export to BigQuery
* quotas
  * GKE API : 1000 requests per 100 seconds
  * 5 networks per project
* can request quota change

# Shared Responsibility
* google responsible for infrastucture
* you must secure your data
  * at least content and access policies (managed services)

# Resource Heirarchy
* Org
* Folders (up to 10 levels)
* Projects  << billing account linked at that level
* Resources

* permissions
  * from high to low
  * so lesser higher up overrides tougher lower down
  * no deny access

* project identifier
  * project id
    * globally unique
    * can be changed at creation only
  * project name
    * not unique
    * mutable
  * project number
    * auto
    * gloally unique
    * internally used
    * immutable


# Next Steps
1. Skills IQ on PluralSight
2. PluralSight: Google Cloud Fundamentals: Core Infrastructure