# Cloud Load Balancing
| Global | Regional |
| --- | --- |
| HTTP(S) | Internal TCP/UDP |
| SSL Proxy | Network TCP/UDP |
| TCP Proxy | Internal HTTP(S) |

# Managed Instance Groups
* identical instances based on same instance template
* used with autoscalar
  * policy
    * cpu
    * load balancing
    * monitoring metrics
    * queue-based workload
* single zone or regional
* can use rolling updates
* recreated instances use same name as former
* type
  * stateless
  * stateful
  * unmanaged
* health check
  * protocol / port / health criteria


# HTTP(S) Load Balancing
* level 7
* hence URL routing
* single anycase global IP 
  * simpler DNS setup
* ports
  * 80
  * 8080
  * 443
* URL maps
  * URL <> instances
* load balancing
  * no pre-warming
  * content based
  * cross regional
* architecture
  1. global forwarding rule directs requests to...
  2. Target HTTP proxy which checks ...
  3. URL Map for right ...
  4. Backend Service which uses
  5. Health Checks to then redirect to right
  6. Backend
* Backend Service
  * health check
  * round robin
    * unless optional session affinity
  * timeout
  * backends
    * instance group
    * balancing mode (CPU or RPS)
    * capacity scalar
      * interacts with balancing mode
      * max % of balancing mode
* if HTTPS
  * at 1 - 10 signed SSL cert on proxy
    * use SSL Resource - only used for load balancers
  * SSL session terminates at load balancer
  * QUIC transport layer supported
    * no head-of-line blocking
    * faster connection
* backend buckets
  * or services
* network endpoint group NEG
  * group of backend endpoints or services
  * used with load balancers and traffic director
  * types
    * zonal
      * one or more endpoints
        * compute engine vms
        * or services running on vms
      * each endpoint an ip address or ip/port
    * internet
      * single endpoint outside of GCP
      * hostname, FQDN, ip/port
    * serverless
      * no endpoints
      * cloud run
      * cloud fn
      * app engine
      * in same region
    * hybrid connectivity
      * traffic director services outside of GCP

# SSL proxy / TCP Proxy Load Balancing


# Network Load Balancing


# Internal Load Balancing