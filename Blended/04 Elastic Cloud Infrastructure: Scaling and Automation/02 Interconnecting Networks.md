# Cloud VPN
* on-prem network to VPS
* 99.9% SLA
* encrypted / decrypted by VPN gateway
  * regional resource
  * physical/virtual device in your network 
* ok for low volume networks
* does not support client dial-in
* must create 2 tunnels
  * each from perspective of its gateway
  * MTU <= 1460 bytes
* cloud router
  * for dynamic routes
  * Border Gateway Protocol
  * can add routes without changing tunnels
  * auto propogate network changes (seamlessly advertised)
  * requires additional external ip on each gateway
    * link local 169.254.0.16
  * dynamic DEPRECATED from Oct 31st
* redundancy by adding second gateway or...
* HA VPN
    * 99.99& SLA
    * must use BGP

# Cloud Interconnect and Peering
* layer 3
  * direct peering
  * carrier peering
  * details:
    * access to GCP services via public ip addresses
    * public ip addresses
* layer 2
  * dedicated InterConnect
  * partner InterConnect
  * details:
    * VLAN direct connectivity in RFC1918 address space
    * internal ip addresses

* Dedicated Interconnect
  * direct physical connections
  * hence common colocation facility
  * BGP session
  * 99.9(9)% SLA
* Partner Interconnect
  * if not near colocation facility
  * supported service provider
* Comparison
  * Cloud VPN: 1.5-3Gps, on prem VPN gateway
  * Partner Interconnect: -10Gps: service provider
  * Dedicated Interconnect: 10-100Gbps, colocated (x 8)
* Peering
  * direct peering between your network and google
  * exchange BGP routes
  * no SLA
  * not near Point of Presence? Carrier


# Sharing VPC Networks
* shared VPC
  * sharing VPC networks across projects
  * cannot share vpc in same project
  * designate a host project and attach others to it
  * centralised admin
* VPC peering
  * RFC1918 connectivity across 2 networks
  * even different organisations
  * decentralised as each newtrok must be set up independently

