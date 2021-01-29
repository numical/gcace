# Networking
* service discovery mandatory
* CNI plugins

## House Rules
* all nodes in a cluster must be able to talk to each other
* all pods can talk *without NAT*
* every pod gets it own IP address
* containers in same pods can talk to each other with localhost

## Network Types
* node
    * 443 (+ more)
    * not implemented by Kubernetes
* pod
    * k8s provides Container Network Interface with plugins implement
    * big and flat
    * pod allocated to node and gets IP address from range allocated to that node
    * pods see itself as external address
* service
    * the IP of services (see below)
    * not really a network
    * kube-proxy pod per node (a daemon set) in IPTABLES mode
        * writes IPTABLE rules from svc address to pod address
    * pod to pod comms
        1. hence pod > service name
        1. DNS converts service name to service IP
        1. sent to virtual ethernet has no idea so sends to default gateway
        1. this is cbr0 (~ docker0) which, as a dumb bridge, passes to eth0
        1. which goes via kernel of host, which uses IPTABLE rules
        1. finally to destination pod address
    * but IPTABLES really for firewalls, not load-balancing so does not scale well, so...
    * new mode: IPVS mode (native in linux kernel - layer 4 load balancer) 
        * different load balancing options
        * more scalable
    * "a set of IPVS or IPTABLE rules that trap on service addresses so that traffic is forwarded to pods on the pod network"
        
    
## Service
* stable abstraction for bunch of pods
* think of as load-balancer/proxy
* 'front end'
    * gets a stable
        * name (DNS)
        * ip
        * optionally a port (see types)
    * registered with CoreDNS
* 'back end'
    * label selector to identify pods
    * how match labels to ip's? use an end-point object
    
### Service Types
* 3 major
    1. LoadBalancer
    1. ClusterIP
        * default
        * only accessible from within cluster
    1. NodePort
        * as above but external access via cluster-wide port  (30000 - 32767) 
        
## Example Code
```
gcloud container clusters get-credentials cluster-1 --zone europe-west1-b --project numical-k8s-lab
kubectl apply -f ./ping-deploy.yml
kubectl get pods -o wide
kubectl exec -it pingtest-7b7bb55f89-8m8mn -- /bin/bash
kubectl get svc --watch
kubectl describe svc hello-svc
```
        
### Notes
Nodeport service:  
```hello-svc    NodePort    10.4.6.46    <none>        8080:30001/TCP   28s```
access with either:
* cluster IP + container port so 10.4.6.46:8080
* any node + node port : <node-ip>:30001