# Core Options
* Cloud Storage
* CLoud SQL
* Cloud Spanner
* Cloud Datastore
* Cloud BigTable

# Cloud Storage
* binary large object storage
* **not**
  * file storage (hierarchy of folders)
  * block storage (chunks of disk) 
* unique key > arbitrary bunch of bytes
* not a file system, instead buckets of storage objects
* storage objects are immutable

## Bucket
* globally unique name
* geographic location
* storage class  << WRONG
  * multi-regional
  * regional
  * nearline
  * coldline 
* IAM or ACL
* versioning
* lifecycle
* contents
  * files (flat namespace)
  * ACL
* get data in
  * gsutil
  * DnD in GCP console
  * storage transfer service
  * transfer appliance
  * import/export
    * BigQuery
    * Cloud SQL

# Cloud SQL
* MySQL or PostgreSQL
* access patterns
  * with app engine using standard drivers
    * 'Cloud SQL instance to follow an App Engine application'
  * compute engine instances can be authorised to access Cloud SQL via external IP address
  * external tools can also access
    * external read replicas too
    
# Cloud Spanner
* SQL too, transactional
* horizontally scalable
* strong global consistency

# Cloud Datastore
* NoSQL
* document datastore
* horizontally scalable
* transactions, SQL-like
* free quota
    
# Cloud BigTable
* NoSQL
* wide-column
* sparsely populated
* ideal for single lookup key
* persistent hashtable
* same API as HBase (Apache Hadoop)
* access patterns
  * app API
  * streaming
  * batch processing

# LAB
`gsutil mb -l US gs://$DEVSHELL_PROJECT_ID`
