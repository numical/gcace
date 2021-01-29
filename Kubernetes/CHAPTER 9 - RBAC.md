# Big Picture
* access to API server
  * client > API > authN > authZ > admission control
* all members of the control plane are clients
  * nodes
  * scheduler
  * controllers
  * kubctl
* authN
* authZ 
* then admission control
  * mutate
  * validate
* then schema validation
* note k8s insecure port if on master - best disable
* deny by default
* default users way too powerful

# AuthN
* default
  * bearer tokens
  * client certs
    * every cluster gets a CA
    * use this to mints user certs
    * embed user names in the CN property
    * groups as organisations
    * create kubectl context so cert embedded in all future commands
  * bootstrap tokens
  * external systems
* no users in k8s
  * have to use external systems such as AD or IAM
* but do have service accounts in k8s for
  * every pod
  * every component of control plane
  * used with auth with APIServer
  
# AuthZ
* generally minimum is 2 modes:
  * RBAC
  * Node (for kubelets to APIServer)
* Subject : who
* Verb: action
* Resource: resource

# RBAC
* deny by default
* no such thing as a deny rule
* Roles
  * rules
    * apiGroups
    * resources
    * verbs
  * bound to namespace
* RoleBindings
  * bound to namespace
* use ClusterRoles and ClusterRoleBindings for cluster-wide  
* optimal: ClusterRoles + namespace-bound RoleBindings

# Admission Control
* new
* webhooks > external admission controller
* two types
  * mutating
  * validating
  
# creating own certs
* openssl genrsa -out example.key 2048
* openssl req -new -key example.key - out example.csr -subj "/CN=username/O=namespace" 
* now cluster's CA to sign request