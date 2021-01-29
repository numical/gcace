# Storage
## High-level Requirements
* decouple storage from pods
* pod lays a claim then mounts volume
* file & block : first class citizen

## CSI
* plugins for k8s
* out-of-tree
* open standard

## Kubernetes Persistent Volume Subsystem
* persistent volumes (PV)
* persistent volume claims (PVC)
    * yaml config must match the PV
        * accessMode
        * storageClassName
        * storage (well claim <= volume)
* access modes
    * RWO
    * RWM (file based only, not block)
    * ROM
    * ony one mode at a time
* reclaim policy
    * delete (when no more claims on volume)
    * retain (default)

## Storage classes (SC)
* makes it dynamic
* SC name: xxx <> PVC storageClassName: xxx, name: YYY <> Pod: persistentVolumeClaim: YYY