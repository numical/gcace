# Cloud Load Balancing
| Global (& ipv6)| Regional |
| --- | --- |
| HTTP(S) e | Internal HTTP(S) |
| SSL Proxy e | Network TCP/UDP e|
| TCP Proxy e | Internal TCP/UDP |

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
  6. Backend service serving
  7. instance group or NEG
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
* SSL
  * global
  * layer 4
  * terminates SSL
  * certificate management - only one place
  * intelligent routing (on load)
  * traffic form proxy to backend can be SSL or TCP
* TCP
  * global
  * layer 4

# Network Load Balancing
* regional
* TCP/UDP
* non-proxied
  * traffic through load balancer
  * client IP preserved
* architecture
  * backend service
    * regional
    * more features - autoscaling, non-legacy 
  * target pool
    * group of instances
    * hash of source ip/port and destination ip/port
    * one health check

# Internal Load Balancing
* regional
* TCP/UDP
* behind private load balancing address
* all within VPC
  * config simpler
  * lower latency
  * software defined, fully distributed
  * built on andromoda

# Internal HTTP(S) Load Balancing
* proxy based
* regional
* open source Envoy proxy