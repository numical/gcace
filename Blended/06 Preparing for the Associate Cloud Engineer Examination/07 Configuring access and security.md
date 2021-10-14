# 5.1 Managing Identify & Access management

# 5.2 Managing Service Accounts
* with limited scopes
* assigning to VM instance
* granting access to service account in another project
* access scopes
  * legacy
  * before IAM roles came along
  * must use for an instance to act as a service account
  * base URL up to auth section
  * must not contradict role
  
# 5.3 Viewing audit logs
* admin activity
* system events
* data access
* write to:
  `[projects|folders|organizations]/[PROJECT_ID]/logs/cloudaudit.googleapis.com%2F[activity|data_access|system_event]`
