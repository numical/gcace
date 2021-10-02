# Concepts
* K8S Object
  * persistent entity representing the state of the cluster
  * Object spec
  * Object status
  * 'kinds' of objects are:
* Pod
  * containers are tightly coupled
  * share networking and storage
  * has unique ip address - shared by all containers
  * 127.0.0.1 'localhost' for communicating within pod
* 

# Control Plane
* various processes that collaborate to make things work
* one vm is control plane, the others are nodes
* components
  * kube-APIserver
    * accept commands
    * authenticates & authorise commands
    * manages admission control
  * etcd
    * database
    * never interact direct with this
  * kube-scheduler
    * does not actually launch - just decides where and writes name of node into pod
    * using hardware, software and policy
  * kube-controller-manager
    * makes changes
    * uses controllers to manage workloads
    * controllers
      * deployments
      * node controllers
  * kube-cloud-manager
    * manages controllers with underlying cloud provider
* each node
  * kubelet
    * agent
    * use container runtime to start pod
      * containerd (docker)
    * monitors lifecycle
    * reports back
  * kube-proxy
    * maintain network connectivity
    * via firewall capabilities of ip tables

# GKE Concepts
* kubeadm to do most of setup
* GKE abstracts away the control plane
* not seperately billed for control plane
* K8S DOES NOT CREATE NODES
* GKE does
* pay per hour
* node pool
  * nodes within a cluster that share a config
* single zone (by default)
  * so use regional cluster - 3 zones by default
* also can be a private cluster
  * gcp access
  * authorized networks

# Object Management
* manifest files
  * yaml
  * json
* name
  * unique to object kind
  * 253 chars
  * alphanumeric, periods, hyphens
* UID
  * no same through life of cluster
* pods are ephemeral & disposable
  * lifecycle is simple - born, running, dies
* use a controller object
  * ReplicaSets
    * keep N identical instances up
  * Deployment
    * long-lived
    * declarative updates to ReplicaSets
  * ReplicationControllers
    * legacy
  * StatefulSets
    * pods get persistent identities
    * stable network identity
  * DaemonSets
    * certain pods on all nodes
    * e.g logging
  * Jobs
    * creates pods to run a task
    * CronJob
* namespaces
  * single physical cluster can be divided
  * resource quotas
  * could also just use labels
  * three namespaces
    * default
    * kube-system
    * kube-public
  * best to apply at command line level
* services
  * load balanced access to specified pods
  * kinds:
    * ClusterIP - ip address ony within cluster
    * NodePort - specific poert number on each node's IP
    * LoadBalancer - expose externally
      * in GKE
        * regional network load balancing
        * for global HTTP(S) load balancing - use Ingress object

# Migrate for Anthos
* moves VM's to containers
* migrate for compute engine
  * on premises to edge nodes + migrate manager
* then migrate for anthos
  * processing cluster
  * artifacts
  * images
* then production project
  * prod cluster
* steps
  1. configure processing cluster
  2. add migration source
  3. generate and review plan
  4. generate artifacts
  5. test
  6. deploy
* 
