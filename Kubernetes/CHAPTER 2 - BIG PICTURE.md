# Overview
* application orchestrator
* open source platform for running cloud-native apps
* cloud agnostic

# Primer
* nodes divided into
    * control plane
        * api server
            * gateway into cluster
            * lots of security
        * scheduler
        * controllers
        * persistent store
            * only state in control plane
            * etcd
    * workers

# API
* everything a resource in the API
* kubectl > post yaml file > record of intent > updates cluster desired state > watch loops pick up change
* yaml files are living application documentation
* core API group - ""
* now many API groups
    * apps


# Objects
## Pods
* k8s does not run containers
* these are wrapped in **pods**
* atomic unit of scheduling
* in core API group
* does nothing for scaling or application release; for that...
## Deployment
* wraps a Pod
* in apps API group
* brings flexibility: scaling / rolling updates etc.

# kubectl useful
* -o yaml

