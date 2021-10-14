# 4.1 Managing compute engine resources
* snapshots are incremental
* IAM roles to share snapshots across projects
* image family for versions


# 4.2 Managing GKE resources
* view current running cluster (node, pods, services)
* browse container image repo
* add/edit/remove node
* add/edit/remove pod
* add/edit/remove service
* management interface
* `kubectl expose deployments nginx --port=80 --type=LoadBlanacer`
* `kubectl get pods -l "app-nginx"`
* `kubectl apply -f xxx.yaml`
* GKE node stuff
  * load-balancing
  * node pools  > managed instance group
  * automatic scaling
  * automtaic upgrades
  * node auto-repair
  * logging & monitoring
* workloads
  * deployment
    * contains replicaset
  * statefulset
    * maintains identity
  * daemonset
* service types:
  * ClusterIp
    * internal to cluster (unlike pod ip's)
  * NodePort
    * every pods has port open
  * LoadBalancer
  * ExternalName

# 4.3 Managing app engine resources  << SMALLIE
* resident
  * manual scaling
* dynamic
  * automatic or dynamic

# 4.4. Managing data solutions  << BIGGIE
* executing queries
* estimatng costs of BigQuery
* backing up and restoring
* reviewing job status of cloud dataproces and BigQuery
* moving objects between buckets
* converting buckets
* setting lifecycle management policies
  * delete
  * setStorageClass
  * conditions:
    * age
    * CreatedBefore
    * isLive
    * MatchesStorageClass
    * NumberofNewerVersions


# 4.5 Managing networking resources
* expand a CIDR block
* RFC1918
* secondary range can be removed/replaced if not in use
* largest /29
* broadest in default / ex-default network is /16


# 4.6 Monitoring and logging
* alerts
* custom metrics
* log sinks
* viewing logs
* cloud diagnostics
* view google cloud status