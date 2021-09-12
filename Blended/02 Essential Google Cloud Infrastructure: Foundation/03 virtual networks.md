# VPC
* network is regions + pops
* region normally has 3 zones

# Projects, networks and subnetworks
## Projects
* quota of 5 networks
## Networks
* isolate systems
  * if in same network can communicate over internal IP's
  * else via external ip's via google edge routers
* modes
  * default
    * one subnet per region
    * default firewall rules
  * auto mode
    * one subnet per region
    * regional IP allocation
    * fixed /20 subnetwork per region
    * expandable up to /16
  * custom mode
    * no default subnets
    * regional IP allocation
    * full control of IP allocation
    * expandable to any RFC1918 size
* do not have ip range - simply aggregation of all constructs within them
* in all regions

## Sub networks
* simply ip address range
* subnetworks can cross zones
* can apply same firewall rule
  * .0 reserved for network
  * .1 reserved for gateway
  * penultimate
  * last: broadcast address
* can expand without shutdown
  * cannot overlap
  * must be inside RFC1918
  * automode can go from /20 to /16
  * can only expand
  * dont make subnets too big, else case CIDR range collisions when
    * using multiple network interfaces
    * peering
    * VPN or other connections

## IP Addresses
* VM's can have internal and external ips addresses
* internal
  * must have one
    * allocated by DHCP from subnet
    * DHCP lease is 24 hrs
    * VM name + IP registered as network-scoped DNS
    * DNS resolution
      * hostname always same (unlike ip)
      * `[hostname].[zone].c.[project-id].internal`
        * name resolution by meta data service on instance
        * internal DNS resolver on 169.254.169.254
        * handles inernal nd routes to public DNS service for others
    * must have one
* external
  * optional
  * assigned from pool (ephemeral) < default
  * reserved (static) < charged if not assigned a VM
  * VM does not know external ip - mapped to internal ip
  * DNS resolution
    * not published automatically - have to use external ip
* alias IP ranges

# Routes & Firewall Rules
* every network has:
  * routes for direct vm to vm comms
  * a default route that directs to destinations outside the network
  * firewalls must also allow this
* so for packet to flow
  * route matches ip address
  * and firewall rule 
* route applies if network and instance tags match
  * but if no instance tags match - applies to all << QUESTION
* VPC is a distributed firewall
  * aka connections are allowed / denied at VM level
  * bidirectional once established
  * implied deny all ingress and allow all egress
* rule:
  * direction
  * source or destination
  * protocol & port
  * action
  * priority
  * (assignment)

# Pricing
* free
  * ingress
  * egress to same zone (through internal ip address)
  * egress to google products
  * egress to different gcp service within same region
* external static ip address
  * unused > standard vm > preemtible vm


# Common network designs
* increased availability with multiple zones
  * 1 region
  * 2 zones
  * 1 vm in ech zone
  * single subnet so single firewall rule
  * improved availability without additional firewall complexity
* globalisation with multiple regions
  * 2 regions
  * each with 1 zone
  * global load balancer for latency and lower costs
  * advise not to give VM external IP's
  * Cloud NAT provides internet access to private instances
    * for patches / updates etc.
    * IAP 35.235.240.0/20
    * regional 
    * outbound only
  * also private google access to google apis and services
    * by subnet basis
    * no effect on instances with external ip addresses