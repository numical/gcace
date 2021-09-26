# Resource Manager
* policies
  * contain
    * roles
    * members
  * set on resources
* org > folder > project > resource
* billing is accumulated from bottom up
* org < billing account < project
* OrganisationAdmin role > ProjectCreator role

# Resources
* global
  * images
  * snapshots
  * networks
* regional
  * external ip address
* zonal
  * instances
  * disks

# Projects
* project name
  * not used by any API
  * human readable
* project number
* project id (application id)

# Quotas
* per project
* rate limit
* regional quota
* prevent
  * runaway consumption
  * billing spikes
  * forces size consideration and periodic review

# Labels and names
* key-value pairs
* up to 64
* scripts
  * bulk operations
  * analysis
* vs tags
  * tags only in instances
  * for networking
  
# Billing
