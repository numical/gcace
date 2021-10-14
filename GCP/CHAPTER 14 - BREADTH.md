# Breadth

## Compute

| What | Where | Type | Pay |
| --- | --- | --- | --- |
| Your Code | Cloud Functions | event driven | usage |
| | App Engine | web applications | usage |
| Your Containers | Cloud Run | HTTP req/res workloads |  usage / provision  |
| | Kubernetes Engine | containerised apps | provision |
| Your systems | Compute Engine | existing systems | provision |

### GCE
* IAAS
* Zonal
* boot-up in 35 seconds
* AWS: EC2
* pay be second (60 second minimum)

### GKE
* previously Google Container Engine
* Regional
* AWS: ECS/EKS
* k8s DNS on by default
* IAM not integrated (unlike AWS)
* pay
    * GCE instances
  

### Cloud Run
* new (not in course!)
* serverless agility for containers
* fully managed
* container image listening on HTTP port
* option to put on top of k8s - Cloud Run on GKE
* can switch between too
    
### App Engine
* PAAS
* Regional
* AWS: Elastic Beanstalk / Heroku
* standard: java/python/php/go
  * GAE specific API's + GCP API's
  * no binaries
* standard 2nd gen: later plus Node
  * GCP API's
  * can have binaries
* flex
  * containers  
  * non HTTP(S) ports
  * slower to respond (mins, not secs)
* Flex for any language
* auto-scales
* more than compute: integrates storage, queues, noSQL etc.
* pay
    * GCE instances

### GCF
* google cloud functions
* FAAS / serverless
* Regional
* AWS: lambda
* java/node/python/go
* every function has http endpoint
* events  
* pay:
    * per 100ms
    

## Storage
* local SSD
* persistent disk
* cloud firestore
* cloud storage

### Local SSD
* 375 GB physically attached to server
* AWS: instance store vols / direct attached storage
* stripe for better performance
* data will be lost when instance shuts down
* pay:
    * per GB-month
    
### Persistent Disk
* block-based storage - so must format
* Zonal
* data encrypted between storage and compute instance
* AWS: elastic block storage / storage area network
* persist + replicated
* provision up front
* snapshots (and machine images) - incremental + global
* not file-based, but can mount multiple read-only
* pay:
    * per GB-month
    * snapshots
    
### Cloud Firestore
* multiple clients write to same file store
* Zonal
* predictable performance
* fully managed
* AWS: Elastic File System / network attached storage
* provision:
  * an instance then accessible to GCE and GKE through NFS
  * TB's standard or premium
* speed:
  * standard: 5000 iops 100-200 Mb per sec
  * premium: 60000 iops 1200 Mb per sec
* primary use: lift and shift
* not backups
* pay for provisioning
  * minimum 1 TB
  
### Cloud Storage
* for huge sizes, speeds
* versioned object storage - in a bucket
* metadata
* events  
* Regional, Multi-Regional, Nearline (< monthly), Coldline (< yearly))
* AWS: S3 / Glacier
* 11 9's
* strongly consistent
* integrated site hosting / CDN
* gsutil 
* gcsfuse to mount as file system
* pay
  * operations
  * GB months
  

## Databases

### Cloud SQL
* MySql or PostGreSQL
* Regional
* AWS: RDS
* auto replication / failover
* have to scale manually (verically and horizontally)
* pay
  * underlying GCE and PD's
  * plus service fees
  
### Cloud Spanner
* outgrown Cloud SQL
* Regional, Multi-Regional,
* strongly consistent
* horizontally scalale - 1000's of nodes 
* stale reads > better than eventual consistency with NoSQL
* CAP theorem < chooses consistency and partition tolerance
* 5 nines availability
* not based on failover
* pay
  * seriously large db's
  * pay for node time
  * $1000's a month

### BigQuery
* if not need transactional, but SQL
* Multi-Regional
* serverless column-store datawarehouse
* AWS: RedShift - sorta the same, so Athena
* scales internally
* pay
  * GB actually scanned, or flat-rate (40k a month)
  * data stored
  * per GB for streamed inserts
* cache'd

### Cloud BigTable
* noSQL, high volumes
* Zonal
* large op & analytical
* wide column-store
* AWS: DynamoDB or Apache Hbase
* supports open-source HBase API
* integrates with Dataflow / DataProc
* scales
  * processing manually

### Cloud Datastore
* auto-scaled NoSQL DB + ACID transactional support
* Regional, Multi-Regional
* AWS: DynamoDB or MongoDB
* queries limited
  * no joins / aggregates / NOT / OR / <>
* auto indexes + manual but can explode
* pay
  * storage used (including indexes)
  * IO ops
* [comparison between BigTable and Cloud Datastore](https://stackoverflow.com/questions/30085326/google-cloud-bigtable-vs-google-cloud-datastore)
  
### Firebase
* nosql document stores
* plus client updated via websockets
* pay
  * spark (free)
  * flame (flat)
  * blaze (usage based)
#### Firebase Realtime DB
* zonal
* huge JSON doc, located in central US
* pay
  * more for GB/month + GB downloaded
#### Cloud FireStore
* multi-regional
* collections of documents
* pay
  * pay for ops and less for storage & transfer
  
## Data Transfer
* web console
* gsutil

### Data Transfer Appliance
* physically ship a rack
* AWS: Snowball
* ingress only

### Storage Transfer Service
* destination a GCS bucket
* source
  * S3
  * HTTP endpoint
  * another GCS bucket
* pay for actions

## External Networking
* public facing
* (but some internal stuff too)
* private ip vs internet routable addresses

### Google Domains
* AWS: route 53
* built-in DNS or point at your own nameservers
* support DNSSEC

### Cloud DNS
* Global
* AWS: route 53
* 100% uptime 
* public managed zones 
* 2019 also private zones

### Static IP
* reserve static IP's
* AWS: elastic IP
* regional IP's for GCE instances and newtork load balancers
* global IP's for global load balancers
* HTTP(S), SSL, TCP
* 'anycast IP' - DNS 'A' service
* pay for unused

### Cloud Load Balancing
* Regional, Global
* integrated with autoscaling & Cloud CDN
* no pre-warming
* based on Andromoda (Google network software)
* regional
  * can do health checks
  * round robin or session affinity
  * forwarding based on ip, protocal and port
* global
  * HTTP(S)/SSL/TCP
  * region nearest user
  * reacts quickly to changes in users/traffic/network/health
  * pay
    * for data ingress too
    * plus hourly per rule
  

### Cloud CDN
* Global
* AWS: Amazon Cloudfront
* HTTP(s)(/2)
* no custom origins
* switch on with simple https load balancer config
* pay
  * cache fill egress charges (cheaper in-region)
  * request volume
  * per cache invalidation request
  * origin costs put low is a good caching strategy
  

## Internal Networking
* private ip addressing
* generally not visible to clients

### Virtual Private Cloud
* global, regional
* ipv4
* sdn
* AWS: Amazon VPC
* modes
  * automatic
  * custom - subnets, routes, firewalls, VPN, BGP (border gateway protocol)
* VPC - global
* subnet - regional
* can be peered with other VPC's
* can enable private IP for some services (GCS)

### Cloud Interconnect
* external networks to google network
* private connections to VPC via Cloud VPN or dedicated interconnect - SLA's

* public services via external peering - no SLA's
* lower egress fees

### Cloud VPN
* Regional
* IPSec VPN to connect VPC via public internet
* low volume connections
* AWS VPN, or OpenVPN
* persistent static connections between gateways (aka not dynamic)
* peer VPN gateway must be static ip
* links to specifc subnet in VPC
* link is encrypted
* three 9's
* static or dynamic routing - the latter is preferred
* pay:
  * tunnel hours
  * traffic

### Dedicated Interconnect
* not encrypted
* direct physical link
* Regional, MultiRegional
  * but not same as elsewhere
  * VLAN attachment in that region
* pay
  * per 10 Gps link
  * small fee per VLAN attachment
  * reduced egress rates
  
### Cloud Router
* using BGP
* if not, have to manage static routes

### CDN Interconnect
* external CDN's - Akamai, CloudFlare, Fastly
* per project and per region
* cheaper for that CDN - should use

## Machine Learning

### Cloud Machine Learning Engine
* scalable service for training ML models & making predictions
* AWS: SageMaker
* based on TensorFlow
* download and use in app

### Cloud Vision API
* AWS: Rekognition
* categorise images
* no provision
* pay
  * per image
  * per feature
  * OCR per document

### Cloud Speech API
* speech to text
* 110 languages
* can stream
* pay per 15 seconds of audio

### Cloud Natural Language API
* understanding language
* pay
  * per 1000 characters
  * per feature
* (text to speech)  
  
### Cloud Translation API
* >100 languages
* semnatics and syntax
* txt or HTML
* pay per character

### DialogFlow
* conversational interfaces
* AWS: lex
* train to identify custom entity types
* 30+ pre-built agents
* pay
  * free for unlimited text + capped voice
  * paid plan charges per request
  

### Cloud Video Intelligence
* annotates videos
* pay per minute


### Cloud Job Discovery


## Big Data & IoT

| Ingest | Store | Process & Analyze | Explore & Visualize |
| --- | --- | --- | --- |
| App Engine | Cloud Storage | Cloud Dataflow | Cloud DataLab|
| Compute Engine | Cloud SQL| Cloud Dataproc | Google Data Studio |
| Container Engine | Cloud Datastore | BigQuery | Google Sheets |
| Cloud Pub/Sub  | Cloud Bigtable | Cloud ML | |
| Stackdriver Logging | BigQuery | other pretrained ML | |
| Cloud Transfer Service | | | |


### Cloud IoT Core
* collect manage and ingest data from devices
* AWS: IoT
* device manager : id, auth, config & control
* protocol bridge > telemetry > cloud pub/sub
* device shadows to deal with devices being offline

### Cloud Pub/Sub
* at least once messaging
* global by default
* topic > subscribers
* AWS: SNS / SQS (notification/queue)
* messages up to 10MB
* push mode to HTTPS endpoints & succeeds on 200 response
* undelivered stored for 7 days
* push mode: slow-start algorithm
* pull mode: client and waits for ACK
* long-polling
* pay
  * data volume
  * each request at least 1Kb

### Cloud Dataprep
* visually explore, clean and prepare
* ad-hoc ETL for business analysis
* Trifacta Wrangler

### Cloud Dataproc
* batch MapReduce - Hadoop & Spark
* AWS Elastic Map Reduce
* integrated with lots
* for existing Spark/Hadoop setups - for new use...
* _not_ streaming data, just batch
* https://cloud.google.com/dataproc

### Cloud Dataflow
* batch or stream MapReduce-like
  * based on Apache Beam
* AWS Elastic Map Reduce, or Apache Beam
* integrated with lots
* can use got batch or streaming
* https://cloud.google.com/dataflow/

### Cloud Datalab
* visualisation
* Jupyter Notebook
* python / SQL / JS for BigQuery defined functions

### Cloud Data Studio
* dashboards / reports
* AWS: QuickSight

## Identity & Access
*  AAA - authn, authz, accounting

### Roles
* collections of permissions
    * service.resource.verb
* AWS: policies
* primitive:
  * owner (access & billing)
  * editor
  * viewer
* predefined:
  * roles/pubsub.subscriber
* custom roles

### Cloud IAM
* authZ
* AWS: IAM
  

### Member
* user  > google account, GSuite/Cloud Identity domain
* group  > google group
* service account > application/instance
* public 'allUsers'
* all have unique email address

### Policy
* bind member to role at a hierarchy leveL
  * org
  * folder
  * project  < a trust boundary
  * resource
  
### Service Accounts
* application, not user
* not API keys or user
* use cloud platform managed keys

### Cloud Identity
* people
* alternatives: GSuite / mltiple gmail accounts / AD
* free google accounts tied to a verified domain
* so manage in google admin console
* can use CloudDirectory sync
* normal accounts

### Security Key Enforcement
* physical keys
* eliminates man-in-the-middle

### Resource Manager
* centrally manage org's projects
* AWS: Organisations
* need a cloud identity domain set up
* else owned by people

### Cloud Identity Aware Proxy
* BeyondCorp security model
* guards apps via identity verification, not network access
* cloud load balancer and IAM cooperate
* AWS: API gateway

### Cloud Audit Logging
* AWS: CloudTrail
  * 400 days unless otherwise stated
* 4 types:
  * admin activity 
  * system events
  * access transparency logs - done by Google
  * data access (30 day)
    * only what Google can see
    * free unless to Stackdriver logging

## Security Management
* monitoring & response
* threats and attacks

### Cloud Armor
* edge level (DDOS etc.)
* AWS: Shield + Web Application Firewall
* only for global HTTPS load balancer
* coordinate across all edges
* blocks attack - never reaches your system
* can check in StackDriver logging
* allow / block lists via CIDR
* more intelligent rules coming
* can use preview
* pay
  * per policy / rule
  * extra per request
  
### Cloud SecurityScaner
* crawler based
* free
* vulnerability scanner

### Cloud Data Loss Prevention API
* redacts sensitive data
* lots of data detectors
* test and images
* stored or streamed

### Event Threat Detection
* AWS: GuardDuty, or Splunk
* can detect active attacks
* unauthorised access to GCP resources via abusive IAM 
* integrate with other services
* free - charged for services used

### Cloud Security Command Center
* security information and event management
* AWS: SecurityHub, Splunk
* free - charged for services used

## Encryption Key Management

### Cloud Key Management Service
* symmetric (AES)
* asymmetric (RSA, EC)
* AWS: KMS
* does not store itself
* integrated with IAM and Cloud Audit logs
* rotates keys
* pay
  * active keys
  * key operations

### Cloud Hardware Security Module
* for compliance
* feature of KMS
* pay
  * active keys
  * key operations
  * much higher


## Operations & Management

### StackDriver
* family of services
* AWS: CloudWatch
* integrates with GCP, each other, and other apps, even AWS accounts
* one account can track multiple projects
* pay
  * usage-based pricing
  
### Stackdriver Monitoring
* based on collectd - uses agent
* cross cloud
* automatic GCP metrics free


### Stackdriver Logging
* store, search, analyze
* AWS CloudWatch / Splunk
* also an API
* realtime metrics 
* send to BigQuery
* pay
  * GB ingested for one month
  * first 50 GB per project free
  * cloud audit logs always free
  

### Stackdriver Error Reporting
* crashes
* aggregates errors
* clean stack traces (main languages)
* just standard Stackdriver Logging

### Stackdriver Trace
* across distributed systems
* AWS: XRay
* GAE automatic
* API's and SDK's for languages
* pay
  * segmenst and scans (..?)
  

### Stackdriver Debugger
* grab program state in live deploys
* uses repos, local or upload
* JS supported on GCE, GKE and GAE Flex only
* auto-enables on GAE else add agents
* can share debug session with co-worker

### Stackdriver Profiler
* cpu and memory
* low overhead 0.5% > 5%
* agent-based
* profiles for 30 days, then download
* no charge

### Cloud Deployment Service
* infrastructure as code
* AWS: CloudFormation
* declarative - yaml
* free

### Cloud Billing API
* programmatically manage billing
* metadata
* not current bill - instead set up export to BigQuery or GCS via console

## Development & API's

### Cloud Source Repos
* hosted private git
* AWS: CodeCommit, Github
* no workflow, instead sync with github
* integration with Stackdriver debugger
* pay
  * per project-user each month
  * storage
  * egress
  
### Cloud Build
* originally container build
* CI/CD service
* AWS: CodeBuild, travis, jenkins
* zip to GCS bucket to kick off
* trigger for Github with Cloud Source Repositories RepoSync
* parallel builds - pay for runtime only
* Dockerfile - build & push
* JSON/yaml describes build steps
* push to Container Registry
* pay
  * pey per minute once over 120 mins per day
  
### Google Container Registry
* fast, private
* AWS: Amazon ECR, DockerHub
* runs a mutli-regional GCS bucket and translates calls
* IAM integration else if external more hassle with auth
* UX integaryed with CloudBuild & StackDriver


### Cloud Endpoints
* handles authz, monitoring, logging, API keys for API's on GCP
* AWS: API Gateway
* distributed (kaka proxies) and hooks into cloud load balancer
* Extensible Service Proxy
* uses JWT's for Google Auth, Auth0, Firebase
* integrates with Stackdriver Logging and Trace
* runs on your instance hence fast (.. unless managed ..?)
* can use gRPC (protocol buffers) - rather than maintain restful
* API must eb resource orientated
* pay per call

### Apigee
* fully featured
* AWS: API Gateway, API Shield
* flat monthly rate


### Test Lab For Android
* AWS Device Farm, SauceLabs


