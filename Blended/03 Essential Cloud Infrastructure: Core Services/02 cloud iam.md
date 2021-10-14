# Overview
* who
* do what
* on which resource


# Organisations
* org > folder > project > resource
* org policy - a config of restrictions
* exceptions but only if user has org admin role
* use conditions - allow access if configures conditions are met
* role
  * org admin
    * define IAM policies
    * determine resource hierarchy
    * delegate responsibility
    * note: not more mundane roles - instead assign additional roles
  * project creator
  * super administrator
    * assign org admins
    * control lifecycle of creating account and org resources

# Folders
* sub-orgs


# Roles
* basic
  * original roles in cloud console
  * course grained
  * types
    * owner
    * editor
    * viewer
    * (also a billing administrator)
* predefined
  * gcp services provide
  * e.g InstanceAdmin - set of permissions
    * service-resource-verb
    * _compute.instances.start_
  * compute engine predefined
    * Compute Admin
    * Network Admin
      * not firewall rules
      * not SSL certs
    * Storage Admin
* custom

# Members
* google accounts
  * any email associated with goosle account - not necessarily gmail
* service accounts
  * can create as many as you want
* google group
  * collection of accounts
* google workspace domain (aka gsuite)
  * org's internet domain name
  * add user creates new account
* cloud identity
  * same capabilities but no gsuite
* **cannot use** Cloud AIM to create or manage users - instead Cloud Identity / GSuite
* Google Cloud Directory Sync
  * AD/LDAP <> users and grouos in Cloud Identity domain
* SSO via SAML2

# Service Account
* belongs to app, not user
* an email `xxx-compute@project.gserviceaccount.com`
* three types
  * user-created
  * built-in (Compute Engine and App Engine have defaults)
  * Google APIs service account
* all project come with:
  * default Compute Engine service account
    * `xxx-compute@developer.gserviceaccount.com`
  * default Google API service account
    * `project-number@cloudservices.gserviceaccount.com`
* use as a resource
  1. create service account with InstanceAdmin role
  2. provision Group/User with ServiceAccountUser role
* how authenticated:
  1. google managed
    * google has both public & private keys
    * can never access private keys
    * max of 2 weeks
  2. user managed
    * google has only public
    * users responsible for private
    * 10 user-managed per service

# Scopes
* legacy method for specifiying permissions for VM
* pre IAM

# Policies
* a list of bindings
* union of parent & resource

# Bindings
* a list of members to a role

# Cloud Identity Aware Proxy
* instead of firewalls
* identity-based for apps accessed via HTTPS
* applied after authentication