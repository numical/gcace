# Deployments
* all about scaling and updates
* actually container <> pod <> (replicaset) <> deployment
* never use replicaset, as deployment will auto-heal etc.
* which pods? - **labels**
* latest config always applied
* replica sets hang around for rollback
* note that pods can be defined in spec manifest, so do not define pods separately

## Updates
* strategy: default is RollingUpdate
* maxSurge: during update
* maxUnavailable - opposite
* minReadySeconds - how long to wait between each
* only changes in template will cause rolling update
* can rollback but not declarative!

## Command
* `kubectl get deploy test --watch` 
* `kubectl rollout status deploy test`
* `kubectl describe deploy test`
* `kubectl get rs -o wide`
* `kubectl apply -f deploy.yml --record`  << adds as annotation on object
* `kubectl rollout history deploy test`
* `kubectl rollout history deploy test --revision=3`
