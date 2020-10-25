#Basic Services
* use projects
* https://cloud.google.com/storage/docs/locations
* quotas
  * user account
  * trail billing account
* Basic unit : bucket 
* IAM vs ACL - run in parallel, aka broader permissions set
* special
  * signed URL's
  * requester pays
  
  
# Commands / Tools
* share same config via gcloud config 
* ReST API > CLI tools > console
* config properties
  * (core/)account
  * (core/)project
  * compute/region
  * compute/zone
* configurations
  * named set of SDK properties

## gcloud
* https://cloud.google.com/sdk/docs/cheatsheet
### syntax
    gcloud <global flags> <service/product> <group/area> <command> <flags> <parameters>
* global flags
  - --help/-h
  - --project <ProjectID>
  - --billing-project
  - --account <Account>
  - --filter (better than grep)
  - --format (JSON, YAML, csv) (note | to 'jq')
  - --quiet/-q
  - --configuration <name>
  - --verbosity
### commands

* config
  * list - all properties in active configuration
  * configurations
    * list - all configurations
    * create <name>
    * activate <name>
    * describe <name>
  * set <property> <value>
  * get-value
  * unset
* init
* projects
  * list
* compute
  * instances
    * list  
  * services
  * list
    * --available / --enabled
  * create
  * delete  
  * ssh
* alpha / beta  
* topic
    
## gsutil (=== 'gcloud storage')
* ls 
  * gs://xxx
  * also '**'  
  * -a 
* mb 
  * -l europe-west2
* label
  * get
  * set - json file
  * ch -l "label:value" 
* versioning
  * get
  * set on
* cp / rm 
* acl

## bq (=== 'gcloud bigquery')

## ssh
* google compute ssh <instance name>
* metadata service
  * https://cloud.google.com/compute/docs/storing-retrieving-metadata
  * curl -H Metadata-Flavor:Google metadata.google.internal/computeMetadata/v1/
* ssh-keygen -t rsa -f ~/.ssh/<private-key-filename> -C <user-name>
  

    
# Console
* separate config to cloud shell
  * e.g. different default zone
* ssh keys automatically passed to created instances
    
    
  
