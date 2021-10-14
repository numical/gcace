###  Cloud function events
  * `gcloud functions deploy {NAME} `
  * http `--trigger-http`
  * pub/sub: `--trigger-topic` `google.pubsub.topic.publish`
  * storage: `--trigger-resource` `google.storage.object.[finalize|delete|archive|metadataUpdate]`
  * firebase `--trigger-event`  `providers/cloud.firestore/eventTypes/document.[create|update|delete|write]`
  * `gcloud functions call`
  * must have a --trigger-xxx
  * 128MB > 8GB
  
### Cloud Logging
  * sinks
    * cloud storage
    * pub.sub
    * bigquery
    * log buckets
  * types
    * _Required
      * 400 day
    * _Default
      * 30 day
    * user-defined
      * 30 day

### DNS records
  * CNAME: canonical name record - specify alias names
  * A: address record: map host name to ip

### App Engine
  * scaling
    * automatic: `target_throughput_utilization`
    * basic: `idle_timeout,max-instances`
    * manual
  * `gcloud app services set-traffic {SERVICE} --splits ...`

###  Cloud Storage
  * IAM roles
    * `roles/storage.objectCreator` : create not view, edit
    * `roles/storage.objectViewer` : view, list
    * `roles/storage.objectAdmin` : anything on objects
    * `roles/storage.admin` : anything on objects and buckets
  * Basic roles
    * `roles/viewer`
    * `roles/editor`
    * `roles/owner`
    * intrinsic behaviour plus ...
    * also adds other accesses through _convenience values_ (which can be changed)
  * Predefined legacy roles
    * equiavlent to ACL permissions
    
### Languages

| Cloud Client Libraries | App Engine Standard | App Engine Flex | Cloud Functions |
| --- | --- | --- | --- |
| Go | Go | Go | Go |
| Java | Java | Java | Java |
| Node | Node | Node | Node |
| Python | Python | Python | Python |
| Ruby | Ruby | Ruby | Ruby |
| PHP | PHP | PHP | PHP |
| C# | | C# | C# |
| C++ | |

### IAM Compute
* `roles/compute.admin`: everything
* `roles/compute.instanceAdmin`: instances 
* `roles/compute.networkAdmin`: network, not firewalls, SSL
* `roles/compute.securityAdmin`: firewalls, SSL
* `roles/compute.storageAdmin`: disks, images, snapshots

### Service Accounts
* compute engine: `{PROJECT_NUMBER}-compute@developer.gserviceaccount.com`
* app engine: `{PROJECT_ID}@appspot.gserviceaccount.com`