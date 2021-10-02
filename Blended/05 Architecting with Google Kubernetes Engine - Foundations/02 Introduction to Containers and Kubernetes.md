# Containers
* virtualisation
  * hypervisor 
    * manages virtual machines
    * just above hardware
    * e.g. KVM
  * multiple apps not isolated
    * therefore seperate vm to each app
    * aka own kernel
  * tied to OS
* containerisation
  * abstraction at app + dependency level
  * virtualise just the user space
  * single container runtime & kernel
  * "isolated userspaces for running application code"
* image
  * a container is a running instance of an image
* linux
  * processes
    * own virtual memory address space
    * rapidly created and destroyed
  * namespaces
    * what app can see 
    * piid, directory trees, ip addresses
    * _not_ same as k8s namespace
  * cgroups
    * control what an app can use
    * cpu / memory / IO bandwidth etc
  * union file systems
    * clean minimal layers
    * using manifest
    * dockerfile - each command creates a layer
    * best practice not to put build tools into image 
      * so use multi-stage build process
    * when launched, container runtime adds writable layer
      * "container layer"
      * ephemeral
* registries
  * gcr.io
  * integrated with IAM so good for private
* docker command
  * must trust the computer
  * or use Cloud Build

## Cloud Build
* from internal & external
* to
  * cloud functions
  * GKE
  * App Engine

# Kubernetes
* network fabric
* container-centric management environment
* imperative only for quick and/or build declarative config
* features
  * stateful & stateful apps
  * batch jobs & daemons
  * autoscaling
  * resource limits
  * extensibility
    * custom resource definitions
  * portability

# GKE
* allow you to bring k8s workloads into the cloud
* fully managed - do not have to configure underlying resources
* container-optimised OS
* start by instantiating a cluster
  * auto-upgrade
  * auto-repair unhealthy nodes
  * k8s can scale workloads, gke can scale cluster itself
  * integration with
    * repos
    * build
    * IAM
    * Stackdriver
    * VPC's
    * cloud console
      * open source k8s has a dashborad - but difficult to set up securely


# Computing Options
Compute engine <> GKE <> App engine <> cloud run <> cloud functions
IaaS <> Hybrid <> PaaS <> stateless <> serverless logic

## Compute Engine
* customisable VM's (up to huge)
* block storage: persistent disks & SSD's
* global load balancing and autoscaling through managed instance groups
* per-second billing
* one container per vm

## GKE
* fully managed k8s platform
* so, on top of k8s:
  * cluster scaling
  * persistent disks
  * automated upgraded
  * auto node repairs
* rich admin of containerised workloads

## App Engine
* fully managed
* zero server mgmt and deployment configuration
* canary testing, version control, rollbacks
* containers run by service (Flexible option)

## Cloud Run
* stateless containers
* knative
* requests or event driven
* abstracts away infrastructure mgmt
* cloud run deploy to fully managed or to own GKE
* 100ms increments

## Cloud Functions
* event-driven, serverless
* triggered on:
  * events on GCP services
  * http endpoints
  * Firebase events


# Notes
* course: "Developing Applications in GCP"