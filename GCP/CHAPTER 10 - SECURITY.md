# Security
* CIA
  * confidentiality - cannot see data you shouldn't
  * integrity - cannot change data you shouldn't
  * availability - can access data you should
* ensuring proper data flow (not too much, not too little)
* AAA
  * authentication - who are you (AuthN)
  * authorisation - what are you allowed to do (AuthZ)
  * accounting - what did you do  (Acct)
* Security Mindset
  * least privilege
  * defense in depth
  * fail securely
* AuthN
  * identity
    * Humans: GSuite, Cloud Identity
    * Apps / Services: Service accounts
  * identity heirarchy
    * google groups
    * (google cloud directory sync to pull from LDAP)
* AuthZ
  * google groups
  * resource heirarchy (organisation, folders , projects)
  * IAM (identity and access management)
    * permissions
    * roles
    * bindings
  * GCS ACLs
  * Billing Management
  * Network structure and restrictions
* Acct
  * audit / activity logs (Stackdriver)  << nb: lots on exam
  * Billing export
    * to BigQuery
    * to file in GCS bucket
  * GCS Object Lifecycle management
  
# IAM Breakdown
* identity and access management 
* AuthZ 
* resource hierarchy
  * resource - something you create
  * project
    * bag of resources
    * behind a trust boundary
  * folder - projects and subfolders
  * organisation 
    *  tied to a GSuite or Cloud identity domain
* permissions
  * <service>.<resource>.<verb>
  * correspond to ReST API calls
* roles
  * collections of permissions
  * primitive roles
    * viewer
    * editor
    * owner : access and billing
  * primitive roles
    * granular access to specific resources
  * custom roles
    * project or org level  
* members
  * google account (email address)
  * service account (email address)
  * google group (email address) << DEFAULT
    * can nest
  * cloud identity / google workspace domain (domain name)
  * allUsers vs allAuthenticatedUsers
* policies
  * bind members to roles for some scope of resources
  * allow only
  * one policy per resource
  * 1500 member bindings per policy (aka use groups)
  * less than 60 secs, up to 7 minutes
  * how change?
    * get-iam-policy, edit, set-iam-policy
    * much better:
    * gcloud <group> add/remove-iam-policy-binding <resource-name> --role <role-id> --member user:<user email>
    * atomic, granular - avoids race conditions
    
# Billing Access Control 
* billing account 
  * outside of projects
  * one billing account for a project
* role: billing account user
  * links projects to billing accounts
* other: billing account creator / administrator / user (as above) / viewer
* to link - require billing account (user role) to project (billing manager)   
* monthly invoiced billing not really an option!
* billing.accounts.getSpendingInformation vs billing.resourceCosts.get
  