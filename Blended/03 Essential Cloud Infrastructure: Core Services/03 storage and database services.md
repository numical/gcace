# Cloud Storage
* time to first byte in milliseconds
* types
  * standard
    * 0 retrieval
  * nearline
    * > 30 days
    * 1c retrieval
  * coldline
    * > 90 days
    * 2c retrieval
  * archive
    * > 365 days
    * 3c retrieval 
* regions
  * multi
  * dual
  * region
* buckets vs object
  * buckets for naming
  * buckets cannot be nested
* access control
  * IAM
  * ACL
    * 100 per object
    * scope + owner/writer/reader
  * signed URL
    * time expired
    * read or write
  * signed policy document
    * mainly to control uploads - size, content type etc.
* other features
  * object lifecycle management
  * object versions
  * directory sync
  * object change notification
    * or added
    * webhook only
    * pub/sub better
  * data import
  * strong global consistency

# Filestore
* managed NAS
* predictable performance
* shared files a sweet spot

# Cloud SQL
* managed
  * patches & updates
  * backup
  * import/export
  * scaling
    * up : restart
    * out: read replicas
* 30 TB, 416GB RAM, 40k IOPS
* max 4000 current connections
* scale out with read replicas
* engines
  * MySQL
  * PostgreSQL
  * MS SQLServer 2017
* HA
  * within region 
* connectivity
  * within GCP, within region > Cloud SQL private IP
  * auto control of SSL certs > Cloud SQL Proxy
  * else manual SSL / authorized networks

# Cloud Spanner
* petabytes
* strong consistency
* automatic replication

# Cloud Firestore
* multi-region replication
* can scale to zero
* Datastore mode
* vs Datastore
  * now strongly consistent, not eventually
  * transaction size not limited
  * writes to entity-group not limited to 1 per sec

# Cloud BigTable
* no transactional consistency
* learns and adjusts to access patterns
* high read/write throughout with low latency
* support HBase API
* massively scalable table - each a key-value map
* column family / column qualifier 
* cells can have multiple versions
* > 1 TB?, < 10 ms latency
* smallest 3 nodes - 30k per sec
* BigTable scales up well, Firestore scales down well

# Cloud MemoryStore
* reddis
* sub-millisecond latency
* 300 GB, 12 Gps