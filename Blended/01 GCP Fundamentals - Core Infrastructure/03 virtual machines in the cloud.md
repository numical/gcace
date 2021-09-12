# Intro
* power & generality of full-fledged OS
* most obvious way to run a workload in GCP

# VPC
* all are global
* subnets are regional
* global distributed firewall
* use tags to link to firewall
* peering VPC between projects OR shared VPC allow full IAM
* cloud load balancing allows single anypoint IP
  * global HTTP(S) : layer 7
  * global SSL proxy: layer 4, non HTTPS, specific port numbers
  * global TCP Proxy: layer 4 non SSL TCP, specific port numbers
  * regional: any traffic, any port numbers
  * regional internal: inside a VPC

# Persistence
* standard
* SSD
* local SSD for scratch space

# VM
* startup scripts
* snapshot of disks

# Interconnect
* VPN - over internet, ipsec protocol (cloud router - border gateway protocol)
* direct peering (router in PoP)
* carrier peering
* dedicated interconnect - SLA

# Lab
* note hostname = {vm name}.{zone}.c.{project oi}.internal