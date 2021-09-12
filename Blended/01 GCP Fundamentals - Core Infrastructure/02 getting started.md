# Basics
1. projects
   1. three identities
      1. project id - unique, chosen by you, immutable  << human readable, use frequently
      2. project name - not unique, chosen by you, mutable
      3. project number - unique, auto assigned (not used in this course)
2. IAM
   * principle of least priviledge
   * policies can be applied at projects, folders and orgs
   * some individual resources too
3. one of several different interfaces to connect

# Heirarchy
* organisation node
  * either auto from g-suite
  * or create manually

# IAM
  * who
    * google account
    * cloud identity user
    * service account
      * control server-to-server interactions
      * id'd by email address
        * {project_number}-compute@developer.gserviceaccount.com
        * {project-id}@appspot.gserviceaccount.com
      * also a resource
    * google group
    * cloud identity or gsuite domain
  * can do what - role
    * primitive
      * broad, fixed
      * owner has billing administrator
    * predefined
      * more fine-grained 
      * particular gcp service 
    * custom
      * need to manage
      * only at project or org level
  * on which resource

# Interaction
1. Cloud Platform Console - web ui
2. Cloud Shell
   1. a temporary VM with Cloud SDK installed
3. Cloud SDK
   1. gcloud
   2. gsutil
   3. bq
   * also a docker image
4. Cloud Console Mobile App
5. ReST-based API
   1. OAuth2
   2. API Explorer

# Cloud Libraries
* Cloud Client Libraries
  * community owned, general
  * more idiomatic
* Google API Client Libraries
  * open source, generated
  * complete
  * older, wrappers to ReST calls

# Cloud Launcher
* any estimated costs do not include network costs
* does not auto-update