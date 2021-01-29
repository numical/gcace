# Meta
* https://learn.acloud.guru/course/gcp-certified-associate-cloud-engineer/dashboard
* https://github.com/gregsramblings/google-cloud-4-words

# Diary
When	What	Planned	How Long
28/09/20
Chapter 1

Chapter 2

16 mins

8 mins

20 mins

20 mins

29/09/20
Chapter 3

Chapter 4

How to Cheat
Products / Services
15 mins

10 mins

45 mins

25 mins

13/10/30
Chapter 4.3

Chapter 5 Getting Started

17 mins

5 mins

30 mins

45 mins


# Resources
https://github.com/gregsramblings/google-cloud-4-words

# Intro
* GCP deeper
* AWS broader
* ACE is running, PCA (professional cloud architect) biz analysis and trade-offs
* 'Cert Prep Guide'


# Exam Guide
* defines scope of role hence of exam hence of course
* scope
  * deploy applications
  * monitor operations
  * maintain to ensure metrics
  * public cloud + on-prem solutions
  * console and CLI
  * leverage google-managed and self-managed
* domains (sections)
  1. setting up a cloud solution environment
     * setting up projects and accounts
     * manage billing config
     * installing and config the CLI
  1. planning & configuring a cloud solution
     * planning and estimating (using pricing calculator)
     * planning and configuring compute
     * planning and configuring data storage
     * planning and configuring network resources
  1. deploying and implementing
     * compute engine resources
     * kubernetes engine
     * app engine and cloud functions
     * data solutions
     * network resources
     * cloud launcher
     * deployment manager
     * CLI
  1. ensuring successful operations
     * managing compute engine
     * kubernetes
     * app engine
     * data solutions
     * network resources
     * monitoring and logging
  1. configuring access and security
     * IAM
     * manage service accounts
     * view audit logs

# Context
* competitors (2015)
  * AWS 90%
  * Azure 5%
  * the rest 5%
* Google about Big Data and innovation
* commercialised internal tools
* uses SRE's, not ops
  * more than half their time building, not op'ing
* from dev > ops, not ops > dev as per AWS
* AWS is a DevOps cloud

# History
* grew internally
  * not originally for Enterprise
* also purchased some - Firebase, StackDriver, Apigee
* playing catch-up, but less tech debt
* willing to be a cloud, not the cloud


# Design & Structure
* principles
  * global
    * intrinsically global - better to handle latency and failure
    * whereas AWS is regional - good for data sovereignty
  * security
    * everything encrypted at rest
    * all control info and WAN encrypted (soon local network as well)
    * distrust the network
      * BeyondCorp
  * scale and automation
    * must be unbounded
    * automate everything
    * resource quotas
      * soft limits
      * regional or global
      * automatic or by request
      * queryable
  * physical infrastructure
    * vCPU
    * physical server
    * rack
    * data center
    * zone (independent of other zones)
    * region
  * multi-region (at least 100 miles away from each other)
    * Europe / Asia / US
  * private global network
    * PoP - network edges and CDN
    * traffic ingress at edge closest to source
    * single global IP load balance across world
  * pricing
    * provisioning: make sure you're ready to handle X
    * usage
    * network traffic
      * free on way in
      * charged on way out
   * egress to other GCP services sometimes free (in general, same region)
* organisation
  * projects
    * primary unit of org
    * similar to AWS account
    * owns resources
    * can be grouped and controlled in a hierarchy 
      
# Products / Services
* see cheat sheet: https://github.com/gregsramblings/google-cloud-4-words
* some cover more than one - e.g. database: storage + processing + transport
* lego analogy
  * Cloud Deployment Manager: lego box + instructions
  * GCP Marketplace: pre-built boxes


# Key Building Blocks
* Compute Engine
  * rent by the second
  * 2x4 brick
* Cloud Functions
  * even finer grained
  * rent by 1/10 of second
  * event driven
  * requests through HTTP
* Kubernetes Engine
* Cloud Storage
  * object based
  * give and receive data
  * nearline / coldline : backups
* Cloud Filestore
  * file based
  * managed NFS server
  * more flexible than cloud persistent disk but works better with some apps than cloud storage
* Cloud Persistent Disk
  * VM-attached disks
  * block storage
  * connect to compute engine
* Cloud TPU
  * tensorflow processing unit
* Cloud SQL
  * MySQL, PostGreSQL
* Cloud Spanner
  * very scalable
* Cloud Firestore
  * strongly consistent serverless document DB
* Cloud datastore
  * pay for what you use
* Cloud Bigtable
  * more predictable
* Cloud Dataflow
  * newer
  * stream & batch
  * apache beam
* Cloud Dataproc
  * hadoop
* Cloud Pub/Sub
  * most flexible global realtime messaging
  * topics publish/subscribe
* Cloud BigQuery
  * crown jewel
  * auto-scaling, very fast
* Virtual Private Cloud
  * the core product
  * others hang off this
* Network Service Tiers
  * single global IP
* Stackdriver
  * management
* Cloud Identity
  * user/devices/apps if not GSuite
* Cloud IAM
  * who can do what to which


# To Do's
* CIDR / subnets - see https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking
* Kubernetes Deep Dive - Nigel Poulton's course 
* 'Official Google Cloud Certified Associate Cloud Engineer Study Guide' in Percipio
