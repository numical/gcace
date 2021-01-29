# First Attempt
48% eek!

## Notes
To look up
* log types, log records
    * request logs
    * application logs
    * flow? logs
* k8s dataset
* region vs multi-region buckets
* ACL's linked to servce account ?
* kubectl syntax
* spanner?
* access scopes
* gcloud init..?
* gcloud containers ..?
* instance types
* nearline vs coldline limits
* access scopes ..??

Cost estimation
SDK setup


PRICING CALCULATOR

## Machine Types
https://cloud.google.com/compute/docs/machine-types#predefined_machine_types
* E2 - cheapest, 4GB, high mem 88GB per vCPU
* N1/N2/N2D - more powerful
* M1/M2 - memory, 24GB per vCPU
* note high cpu are 1GB per vCPU

For reference, the n1-highmem-8 has 8 CPUs and 52 GB of memory, but you do NOT need to remember this. 
Just remember that predefined machine types are named by their CPU counts and those are always powers of two  
--so n1-highmem-10 is invalid. 
Custom machine types let you tweak the predefined types, but you can’t add more RAM per CPU than you get with 
the highmem machine types unless you use “Extended Memory”. 
But since the 8-CPU custom type option does not include --custom-extensions, it doesn’t get Extended Memory 
and the command won’t work. 
Since you’ll need to add more CPUs, you could go to n1-highmem-16--but a custom machine type with only 10 CPUs 
will be less expensive than that.

## Links to review

### Security
* https://cloud.google.com/docs/enterprise/best-practices-for-enterprise-organizations 
* https://cloud.google.com/iam/docs/understanding-service-accounts
* https://cloud.google.com/iam/docs/granting-roles-to-service-accounts
check about ACL's!
also confusion with scopes

### Service Account emails
* default GCE service account: PROJECT_NUMBER-compute@developer.gserviceaccount.com
* default App Engine service account: PROJECT_ID@appspot.gserviceaccount.com
* custom service account: SERVICE_ACCOUNT_NAME@PROJECT_ID.iam.gserviceaccount.com

### Pricing Calculator
* https://cloud.google.com/products/calculator/

### Containers
* https://cloud.google.com/solutions/best-practices-for-operating-containers

### K8S
* https://kubernetes.io/docs/reference/kubectl/cheatsheet/
* https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-intro/
* https://cloud.google.com/stackdriver/docs/solutions/gke
* https://stackoverflow.com/questions/41732819/why-statefulsets-cant-a-stateless-pod-use-persistent-volumes
* https://cloud.google.com/kubernetes-engine/docs/how-to/stateful-apps

### Logging
https://cloud.google.com/vpc/docs/using-flow-logs << 
https://cloud.google.com/appengine/docs
https://cloud.google.com/logging/docs/audit/
https://cloud.google.com/compute/docs/logging/audit-logging
https://medium.com/google-cloud/how-to-log-your-application-on-google-compute-engine-6600d81e70e3
https://cloud.google.com/logging/docs/agent/configuration (skim)

## BigTable
https://cloud.google.com/bigtable/

### Tools
https://cloud.google.com/sdk/docs/initializing
https://cloud.google.com/compute/docs/instances/checking-instance-status