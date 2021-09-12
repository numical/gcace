# Google Kubernetes Engine
* IaaS + PaaS

# Containerisation
* VM virtualises hardware (via Hypervisor)
* offer independent scalability of workloads (PaaS)
* plus abstraction of hardware (IaaS)
* container starts as fast as a process (aka an instance of a running program)
* in essence viruaising OS, not Hardware
* most common format - Docker
* alternative - Cloud Build

# Kubernetes
* k8s node === GCP vm instance
* GKE - managed service
* `gcloud container clusters create k1`
* pod == virtual ethernet > container(s) < volume(s)
* `kubectl run nginx --image=nginx:1.15.7`
* deployment = group of replicas of same pod
* `kubectl get pods`
* make pubic by connecting load balancer
* `kubectl expose deployments nginx --port=80 --type=LoadBalancer`
* this
  * creates a 'service' > how k8s represents load balancing
  * attaches a public network load balancer with fixed public ip
* service group - set of pods with stable endpoint
* `kubectl get services`
* scaling
  * `kubectl scale nginx --replicas=3`
  * `kubectl autoscale nginx --min=10 --max=15 --cpu=80`
* declarative better than imperative
* `kubectl get pods -l "app=nginx -o yaml`
  * also get `replicasets`, `pods`, `services`
* `kubectl apply -f nginx-deployment.yaml`
* a deployment has a an update strategy

# Hybrid
* Anthos
  * k8s
  * GKE On-Prem
  * single control plane
  * lots of management tools
* linked to Google MarketPlace
* Anthos service mesh < cloud interconnect > istio service mesh
* anthos config stores in policy repo - a git repo
* stackdriver for all mogging and monitoring