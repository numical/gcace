# Networking

## Routing
* software defined networking
* OSI 7 - conceptual only
  * layers 1-4 lower: moving data around
  * layer 5-7 upper: application-level data
  * APSTNDP
    - 7 Application - HTTP
    - 6 Presentation - encoding: ASCII
    - 5 Session - connections between apps
    - 4 Transport - flow control / recovery: TCP
    - 3 Network - routing: IP
    - 2 Data Layer - data packest > bits
    - 1 Physical 
* local decisions, no full map
* Routing To Google's Network
  * premium vs standard
  * hot potatoe routing makes it someone else's problem
* Routing to the right resource
  * latency reduction
    * global anycast IP
    * cross-region load balancing
  * load balancing
    * not same as auto-scaling
    * cloud load balancer (internal/external)
  * system design
    * http(s) load balancer (with URL map)
  * routing schemes
    * unicast < normal
    * anycast < google specific
  * level 4 load balancing
    * TCP
    * aka ip addresses only
    * hence cannot use path
    * could you use DNS?
      * DNS queries very chunky and cached
      * DNS lookups sticky (TTL)
      * layer 4 only
      * not robust
  * level 7 load balancing
    * can use path    
* Routing from one resource to another
  * VPC
    * your private SDN in GCP
    * covers doors
    * global
  * subnets 
    * regional
    * but all connected (data transfer charges)
  * routes
    * also global
    * define next hop based on destination IP
    * network tags on GCE instances to define whether route applies to it
    * so do not define route, use tags
    * if no route on internet gateway, data will not flow
    * *might* be able to connect, coz also
  * firewall rules
    * global
    * but applied by instance-level tags
    * or service account
    * default are restrictive in, permissive out
    
## VPC
* auto mode
  * one subnet in every region
  * some default firewall rules
  * new regions auto-created
  * no IP ranges for VPC itself
* custom mode
  * create own subnets
* custom service account
  * no access scopes
* do not use subnets for security  
* cross region costs money 
* can share across projects
  * host project
  * service projects

### Firewall Rules
* all config should work irrespectibe of zone, region or subnet
* security based on intention, not location
* ingress
  * ends in VPC
  * can use to stop service accounts (etc.) accessing anything as apply to all, deny, from service-account
* egress
  * starts in VPC
  * use these for internet
* both if from VPC to VPC

## Exam Tips
* CIDR blocks and port numbers

## Command line
* from https://acloud.guru/forums/gcp-certified-associate-cloud-engineer/discussion/-MFp9W0rEdUqba6PuDkO/Challenge-Lab-Resolution-10-and-a-call-for-collaboration

```
#: setting region  
gcloud config set compute/region us-west1 

#: creating the VPC 01 
gcloud compute --project=pimballeke-new-project005 networks create wb01 --description=wb01 --subnet-mode=custom  

#: listing VPCs  
gcloud compute --project=pimballeke-new-project005 networks list  

#: creating two subnets  
gcloud compute --project=pimballeke-new-project005 networks subnets create wb01-subnet-a \
--network=wb01 --region=us-west1 --range=192.168.0.0/24  

gcloud compute --project=pimballeke-new-project005 networks subnets create wb01-subnet-b \
--network=wb01 --region=us-west1 --range=192.168.1.0/24  

gcloud compute --project=pimballeke-new-project005 networks subnets create wb01-subnet-c \
--network=wb01 --region=us-west1 --range=192.168.2.0/24  

#: listing subnets  
gcloud compute networks subnets list  
NAME           REGION    NETWORK  RANGE  
wb01-subnet-a  us-west1  wb01     192.168.0.0/24  
wb01-subnet-b  us-west1  wb01     192.168.1.0/24  
wb01-subnet-c  us-west1  wb01     192.168.2.0/24

#: Create the Custom Role named Base GCP Role wrapping the Logs Writer, Monitoring Metric Writer permissions  
gcloud iam roles create BaseGCERole102 --project=pimballeke-new-project005 --title=BaseGCERole102 \
--description="BaseGCERole102" --stage="GA" \
--permissions=logging.logEntries.create,monitoring.metricDescriptors.create,monitoring.metricDescriptors.get,monitoring.metricDescriptors.list,monitoring.monitoredResourceDescriptors.get,monitoring.monitoredResourceDescriptors.list,monitoring.timeSeries.create

#: list the created role  
gcloud iam roles list --project $(gcloud config get-value project)  
Your active configuration is: [cloudshell-27980]  
---  
description: BaseGCERole102  
etag: BwWvrOuC1Ak=  
name: projects/pimballeke-new-project005/roles/BaseGCERole102  
stage: GA  
title: BaseGCERole102  

#: Create the fronted-sa and the backend-sa service accounts (compute engines and firewall rules runs with them)    
gcloud iam service-accounts create frontend-sa --display-name "frontend-sa"    
gcloud iam service-accounts create backend-sa --display-name "backend-sa"    

#: listing service-accounts    
gcloud iam service-accounts list    
DISPLAY NAME  EMAIL                                                          DISABLED    
frontend-sa   frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com  False    
backend-sa    backend-sa@pimballeke-new-project005.iam.gserviceaccount.com   False    

#: add policy binding stating the role previously created    
gcloud iam service-accounts add-iam-policy-binding frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com --member='user:email@gmail.com' \  
--role='projects/pimballeke-new-project005/roles/BaseGCERole102'  

gcloud iam service-accounts add-iam-policy-binding backend-sa@pimballeke-new-project005.iam.gserviceaccount.com --member='user:email@gmail.com' \  
--role='projects/pimballeke-new-project005/roles/BaseGCERole102'    

#: liting bindings to our service accounts    
gcloud iam service-accounts get-iam-policy frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com    
bindings:    
- members:    
  - user:pimballeke@gmail.com    
  role: projects/pimballeke-new-project005/roles/BaseGCERole100    
etag: BwWvq5fZYAI=    
version: 1    

gcloud iam service-accounts get-iam-policy backend-sa@pimballeke-new-project005.iam.gserviceaccount.com    
bindings:    
- members:    
  - user:pimballeke@gmail.com    
  role: projects/pimballeke-new-project005/roles/BaseGCERole100    
etag: BwWvq5kc5YA=    
version: 1    

#: Create the Instance Templates frontend-it and the backend-it  
gcloud compute instance-templates create frontend-it --machine-type=f1-micro --tags=open-ssh-tag \  
--network=wb01 --subnet=wb01-subnet-a --service-account=frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com    

Created [https://www.googleapis.com/compute/v1/projects/pimballeke-new-project005/global/instanceTemplates/frontend-it].    
NAME         MACHINE_TYPE  PREEMPTIBLE  CREATION_TIMESTAMP    
frontend-it  f1-micro                   2020-09-19T07:45:16.585-07:00    

gcloud compute instance-templates create backend-it --machine-type=f1-micro \  
--network=wb01 --subnet=wb01-subnet-a --service-account=backend-sa@pimballeke-new-project005.iam.gserviceaccount.com    

Created [https://www.googleapis.com/compute/v1/projects/pimballeke-new-project005/global/instanceTemplates/backend-it].    
NAME        MACHINE_TYPE  PREEMPTIBLE  CREATION_TIMESTAMP    
backend-it  f1-micro                   2020-09-19T07:47:08.354-07:00  

#: listing instance-templates  
gcloud compute instance-templates list  
NAME         MACHINE_TYPE  PREEMPTIBLE  CREATION_TIMESTAMP  
backend-it   f1-micro                   2020-09-19T09:20:00.557-07:00  
frontend-it  f1-micro                   2020-09-19T09:19:25.564-07:00

#: frontend 
gcloud beta compute --project=pimballeke-new-project005 instance-groups managed create frontend-ig \
--base-instance-name=frontend-ig --template=frontend-it --size=3 --zones=us-west1-a,us-west1-b,us-west1-c \
--instance-redistribution-type=PROACTIVE

Created [https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1/instanceGroupManagers/frontend-ig].  
NAME         LOCATION  SCOPE   BASE_INSTANCE_NAME  SIZE  TARGET_SIZE  INSTANCE_TEMPLATE  AUTOSCALED  
frontend-ig  us-west1  region  frontend-ig         0     3            frontend-it        no  

gcloud beta compute --project "pimballeke-new-project005" instance-groups managed set-autoscaling "frontend-ig" \
--region "us-west1" --cool-down-period "60" --max-num-replicas "3" --min-num-replicas "2" \
--target-cpu-utilization "0.1" --mode "on"  

Created [https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1/autoscalers/frontend-ig-bbwt].  
---  
autoscalingPolicy:  
  coolDownPeriodSec: 60  
  cpuUtilization:  
    utilizationTarget: 0.1  
  maxNumReplicas: 3  
  minNumReplicas: 2  
  mode: ON  
creationTimestamp: '2020-08-26T12:40:41.379-07:00'  
id: '628738619668628566'  
kind: compute#autoscaler  
name: frontend-ig-bbwt  
region: https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1  
selfLink: https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1/autoscalers/frontend-ig-bbwt  
status: PENDING  
target: https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1/instanceGroupManagers/frontend-ig  

#: list instances
gcloud compute instances list  
NAME              ZONE        MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP    STATUS  
frontend-ig-fjdf  us-west1-a  f1-micro                   192.168.0.3  35.247.23.188  RUNNING  
frontend-ig-wbql  us-west1-b  f1-micro                   192.168.0.2  34.82.135.118  RUNNING  
frontend-ig-8tjw  us-west1-c  f1-micro                   192.168.0.4  34.105.89.175  RUNNING  

#: backend  
gcloud beta compute --project=pimballeke-new-project005 instance-groups managed create backend-ig \
--base-instance-name=backend-ig --template=backend-it --size=3 --zones=us-west1-a,us-west1-b,us-west1-c \
--instance-redistribution-type=PROACTIVE  

Created [https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1/instanceGroupManagers/backend-ig].  
NAME        LOCATION  SCOPE   BASE_INSTANCE_NAME  SIZE  TARGET_SIZE  INSTANCE_TEMPLATE  AUTOSCALED  
backend-ig  us-west1  region  backend-ig          0     3            backend-it         no  

gcloud beta compute --project "pimballeke-new-project005" instance-groups managed set-autoscaling "backend-ig" \
--region "us-west1" --cool-down-period "60" --max-num-replicas "3" --min-num-replicas "2" \
--target-cpu-utilization "0.1" --mode "on"  

Created [https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1/autoscalers/backend-ig-y45r].  
---  
autoscalingPolicy:  
  coolDownPeriodSec: 60  
  cpuUtilization:  
    utilizationTarget: 0.1  
  maxNumReplicas: 3  
  minNumReplicas: 2  
  mode: ON  
creationTimestamp: '2020-08-26T12:43:46.822-07:00'  
id: '5381689342276863389'  
kind: compute#autoscaler  
name: backend-ig-y45r  
region: https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1  
selfLink: https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1/autoscalers/backend-ig-y45r  
status: PENDING  
target: https://www.googleapis.com/compute/beta/projects/pimballeke-new-project005/regions/us-west1/instanceGroupManagers/backend-ig  

#: list instances from the MIG  
gcloud compute instances list  
NAME              ZONE        MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS  
backend-ig-cr5j   us-west1-a  f1-micro                   192.168.2.3  34.105.105.41   RUNNING  
frontend-ig-fjdf  us-west1-a  f1-micro                   192.168.0.3  35.247.23.188   RUNNING  
backend-ig-2sz4   us-west1-b  f1-micro                   192.168.2.4  104.198.102.15  RUNNING  
frontend-ig-wbql  us-west1-b  f1-micro                   192.168.0.2  34.82.135.118   RUNNING  
backend-ig-mrph   us-west1-c  f1-micro                   192.168.2.2  34.83.30.166    RUNNING

#: setting firewall rules for frontend 
#: accept incoming ping form the internet  
gcloud compute firewall-rules create allow-external-icmp-fwr --network wb01 --allow icmp \
--target-tags open-ssh-tag --source-ranges 0.0.0.0/0 --priority=100  

#: accept ssh from the internet  
gcloud compute firewall-rules create allow-external-ssh-fwr --network wb01 --allow tcp:22 \
--target-service-accounts frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--source-ranges 0.0.0.0/0 --priority=101

#: can connect (icmp) frontend to backends and vice-versa  
gcloud compute firewall-rules create allow-internal-frontend-to-backend-icmp-fwr --network wb01 --allow icmp \
--source-service-accounts frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--target-service-accounts backend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--priority=102

#: allow ssh from the frontend to the backend  
gcloud compute firewall-rules create allow-internal-frontend-to-backend-ssh-fwr --network wb01 --allow tcp:22 \
--source-service-accounts frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--target-service-accounts backend-sa@pimballeke-new-project005.iam.gserviceaccount.com\
--priority=103

#: allow ssh from the frontend to the backend  
gcloud compute firewall-rules create allow-internal-backend-to-frontend-ssh-fwr --network wb01 --allow tcp:22 \
--source-service-accounts backend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--target-service-accounts frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--priority=104

#: listing firewall-rules  
gcloud compute firewall-rules list  
NAME                                         NETWORK  DIRECTION  PRIORITY  ALLOW   DENY  DISABLED  
allow-external-icmp-fwr                      wb01     INGRESS    100       icmp          False  
allow-external-ssh-fwr                       wb01     INGRESS    101       tcp:22        False  
allow-internal-backend-to-frontend-ssh-fwr   wb01     INGRESS    104       tcp:22        False  
allow-internal-frontend-to-backend-icmp-fwr  wb01     INGRESS    102       icmp          False  
allow-internal-frontend-to-backend-ssh-fwr   wb01     INGRESS    1000      tcp:22        False  

#: setting firewall rules for backends  

#: deny backends ping to frontends  
gcloud compute firewall-rules create deny-internal-frontend-to-backend-icmp-fwr --network wb01 --action deny \
--rules icmp --source-service-accounts backend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--target-service-accounts frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--priority 10

#: deny web traffic  
gcloud compute firewall-rules create deny-backend-external-traffic-fwr --network wb01 --direction egress --action deny \
--rules tcp:80 --target-service-accounts backend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--priority 11

#: backends pinging backends  
gcloud compute firewall-rules create allow-internal-backend-to-backend-icmp-fwr --network wb01 --allow icmp \
--source-service-accounts backend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--target-service-accounts backend-sa@pimballeke-new-project005.iam.gserviceaccount.com \
--priority 12

#: listing firewall-rules  
gcloud compute firewall-rules list  
NAME                                         NETWORK  DIRECTION  PRIORITY  ALLOW   DENY    DISABLED  
allow-external-icmp-fwr                      wb01     INGRESS    100       icmp            False  
allow-external-ssh-fwr                       wb01     INGRESS    101       tcp:22          False  
allow-internal-backend-to-backend-icmp-fwr   wb01     INGRESS    12        icmp            False  
allow-internal-backend-to-frontend-ssh-fwr   wb01     INGRESS    104       tcp:22          False  
allow-internal-frontend-to-backend-icmp-fwr  wb01     INGRESS    102       icmp            False  
allow-internal-frontend-to-backend-ssh-fwr   wb01     INGRESS    1000      tcp:22          False  
deny-backend-external-traffic-fwr            wb01     EGRESS     11                tcp:80  False  
deny-internal-frontend-to-backend-icmp-fwr   wb01     INGRESS    10                icmp    False

#: exception firewall-rules - ssh to backends to test traffic to frontends 
gcloud compute firewall-rules create allow-external-ssh-exception-backends-fwr --network wb01 --allow tcp:22 \
--target-service-accounts backend-sa@pimballeke-new-project005.iam.gserviceaccount.com --source-ranges 0.0.0.0/0

$ gcloud compute firewall-rules list  
NAME                                         NETWORK  DIRECTION  PRIORITY  ALLOW   DENY    DISABLED  
allow-external-icmp-fwr                      wb01     INGRESS    100       icmp            False  
allow-external-ssh-exception-backends-fwr    wb01     INGRESS    1000      tcp:22          False  
allow-external-ssh-fwr                       wb01     INGRESS    101       tcp:22          False  
allow-internal-backend-to-backend-icmp-fwr   wb01     INGRESS    12        icmp            False  
allow-internal-backend-to-frontend-ssh-fwr   wb01     INGRESS    104       tcp:22          False  
allow-internal-frontend-to-backend-icmp-fwr  wb01     INGRESS    102       icmp            False  
allow-internal-frontend-to-backend-ssh-fwr   wb01     INGRESS    1000      tcp:22          False  
deny-backend-external-traffic-fwr            wb01     EGRESS     11                tcp:80  False  
deny-internal-frontend-to-backend-icmp-fwr   wb01     INGRESS    10                icmp    False

#: VPC Challenge Lab Resolution - Clean Up    

#: set the region    
gcloud config set compute/region us-west1    
Updated property [compute/region].  

#: delete instance-groups (this command shouldn't ask you for --region at this point)  
gcloud compute instance-groups managed delete -q backend-ig --region us-west1  
gcloud compute instance-groups managed delete -q frontend-ig --region us-west1  

#: delete instance-templates  
gcloud compute instance-templates delete -q backend-it  
gcloud compute instance-templates delete -q frontend-it  

#: list and remove subnets    
gcloud compute networks subnets list                                                                                 
NAME           REGION    NETWORK  RANGE    
wb01-subnet-a  us-west1  wb01     192.168.0.0/24    
wb01-subnet-b  us-west1  wb01     192.168.1.0/24    
wb01-subnet-c  us-west1  wb01     192.168.2.0/24    

#: remove all subnets  
for i in {a,b,c}; do gcloud compute networks subnets delete -q wb01-subnet-$i; done

Deleted [https://www.googleapis.com/compute/v1/projects/pimballeke-new-project005/regions/us-west1/subnetworks/wb01-subnet-a].

Deleted [https://www.googleapis.com/compute/v1/projects/pimballeke-new-project005/regions/us-west1/subnetworks/wb01-subnet-b].

Deleted [https://www.googleapis.com/compute/v1/projects/pimballeke-new-project005/regions/us-west1/subnetworks/wb01-subnet-c].  

#: listing firewall-rules  
gcloud compute firewall-rules list  
NAME                                         NETWORK  DIRECTION  PRIORITY  ALLOW   DENY    DISABLED  
allow-external-icmp-fwr                      wb01     INGRESS    100       icmp            False  
allow-external-ssh-exception-backends-fwr    wb01     INGRESS    1000      tcp:22          False  
allow-external-ssh-fwr                       wb01     INGRESS    101       tcp:22          False  
allow-internal-backend-to-backend-icmp-fwr   wb01     INGRESS    12        icmp            False  
allow-internal-backend-to-frontend-ssh-fwr   wb01     INGRESS    104       tcp:22          False  
allow-internal-frontend-to-backend-icmp-fwr  wb01     INGRESS    102       icmp            False  
allow-internal-frontend-to-backend-ssh-fwr   wb01     INGRESS    1000      tcp:22          False  
deny-backend-external-traffic-fwr            wb01     EGRESS     11                tcp:80  False  
deny-internal-frontend-to-backend-icmp-fwr   wb01     INGRESS    10                icmp    False  

#: removing all firewall-rules (only commands)  
gcloud compute firewall-rules delete -q allow-external-icmp-fwr                        
gcloud compute firewall-rules delete -q allow-external-ssh-exception-backends-fwr      
gcloud compute firewall-rules delete -q allow-external-ssh-fwr                         
gcloud compute firewall-rules delete -q allow-internal-backend-to-backend-icmp-fwr     
gcloud compute firewall-rules delete -q allow-internal-backend-to-frontend-ssh-fwr     
gcloud compute firewall-rules delete -q allow-internal-frontend-to-backend-icmp-fwr    
gcloud compute firewall-rules delete -q allow-internal-frontend-to-backend-ssh-fwr     
gcloud compute firewall-rules delete -q deny-backend-external-traffic-fwr              
gcloud compute firewall-rules delete -q deny-internal-frontend-to-backend-icmp-fwr     

#: remove the VPC    
gcloud compute networks list    
NAME  SUBNET_MODE  BGP_ROUTING_MODE  IPV4_RANGE  GATEWAY_IPV4    
wb01  CUSTOM       REGIONAL    

#: remove the VPC  
gcloud compute networks delete -q wb01  

#: remove bidings  
gcloud iam service-accounts remove-iam-policy-binding frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com \  
--member="user:pimballeke@gmail.com" --role=BaseGCERole100  
gcloud iam service-accounts remove-iam-policy-binding backend-sa@pimballeke-new-project005.iam.gserviceaccount.com \  
--member="user:pimballeke@gmail.com" --role=BaseGCERole100  

#: remove role  
gcloud iam roles delete -q BaseGCERole100 --project pimballeke-new-project005  

#: remove service accounts    
gcloud iam service-accounts delete -q backend-sa@pimballeke-new-project005.iam.gserviceaccount.com    
gcloud iam service-accounts delete -q frontend-sa@pimballeke-new-project005.iam.gserviceaccount.com
```
  
  

