* 3 projects
    * networking - owns VPC
    * persistence
    * runtime
* K8s
    * use namespaces rather than clusters to save money
* security - divide
  * human users < via groups
  * service accounts
  * Cloud IAP for admin functions?

* Hierarchy of setup
  * Paying
  * Securing
    * service accounts
    * groups
  * Remembering
  * Moving
    * firewall
  * Processing
    * templates