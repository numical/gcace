# 2.1 Planning and estimating using the pricing calculator


# 2.2 Planning and configuring compute resources
* different workloads
  * compute engine
  * GKE
  * app engine


# 2.3 Planning and configuring data storage options


# 2.4 Planning and configuring network resources
* load balancing
  * differences
    * target pools - level 4 only, forwarding rules
    * managed instance groups - autoscaling, link to target pools 
    * backend service - definitely layer 7 (http) - also layer 4?
* resource locations
* cloud DNS

Create cloud load balancer

1 Create startup script
`gcloud compute instance-templates create nginx-template --metadata-from-file startup-script=startup.sh`

2 Create instance template
`gcloud compute instance-templates create nginx-template --metadata-from-file startup-script=startup.sh`

3 Create managed instance group
`gcloud compute instance-groups managed create nginx-group --base-instance-name nginx --size 2 --template nginx-template`

4 Add named port to the instance group
`gcloud compute instance-groups managed set-named-ports nginx-group --named-ports http:80`

5 Create an http health check
`gcloud compute http-health-checks create http-basic-check`

6 Create a backend service
`gcloud compute backend-services create nginx-backend --protocol HTTP --http-health-checks http-basic-check --global`

7 Add instance group as backend for backed service
`gcloud compute backend-services add-backend nginx-backend --instance-group nginx-group --instance-group-zone us-central1-a --global`

8 Create a URL map that defaults to the backend service
`gcloud compute url-maps create web-map --default-service nginx-backend`

9 Create an HTTP target proxy to route to this URL map
`gcloud compute target-http-proxies create http-lb-proxy --url-map web-map`

10 Create a global forwarding rule to send requests to proxy
`gcloud compute forwarding-rules create http-content-rule --global --target-http-proxy http-lb-proxy --ports 80`



