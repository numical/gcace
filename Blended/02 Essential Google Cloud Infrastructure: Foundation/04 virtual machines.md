# General
* 1 vCPU =  1 hardware hyperthread
* network > 2 Ggbs per vCPU

# Access
* Linux - SSH, require tcp:22 firewall rule
* Windiws - RDP, require tcp:3389 firewall rule

# Lifecycle
1. provisionining
2. staging
   1. includes booting
3. running
   1. included startup script
4. stoping
5. terminated
   1. still charged for attached disks

* shutdown script 90 secs
* if preemtible ACPI power off after 30 secs

# Availability Policy
* 'scheduling options' in SDK/API
* automatic restart
* on host maintenance
* live migration

# Compute Options
* `gcloud compute instances create ...`
* standard machine types
  * 1-96 vCPU
  * 3.75GB per vCPU
  * 1-128 persistent disks (up to 64TB)
* high memory
  * 6.5GB per vCPU
* high CPU
  * 0.9 GB per vCPU
* memory optimised
  * >14GB per vCPU
  * but big - from 40 vCPU's 
* compute optimised
  * 4 GB per vCPU
  * fast processors
* custom
  * 1 or even vCPU's
  * 0.9 > 6.5 GB per vCPU - must be multiple of 256MB

# Pricing
* 60secs then per sec
* discounts
  * sustained (automatic)
  * committed
  * pre-emptible
    * 24 hour max
    * 30 second terminate
    * no auto-restart but other ways (e.g. load balancers)

# Shielded VM's
* verifiable integrity
* select a shielded image

# Image
* consists of
  * boot loader
  * OS
  * file system structure
  * software
  * customisations
* premium images (per sec charges)
* machine image can be used for many scenarios - config & data
* good for backup
  * differential
  * multiple disks
* still in beta

# Disks
* boot
* persistent
  * attached via network
  * can attach multiple VM if read-only
  * types
    * standard
    * balanced (also ssd)
    * ssd
* local
  * ephemeral
  * upto 8 x 375GB 
  * survives reset
  * cannot be attached to different VM
* RAM 

# Common Actions
* metadata server
  * startup scripts
  * shutdown scripts
* move to new zone
  * `gcloud compute instances move` (within region)
  * between regions - manual
* snapshots
  * backup
  * migrate data between zones
  * transfer data to different disk type
  * incremental
  * not metadata
* resize persistent disk - bigger only