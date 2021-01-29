# Auto-Scaling

# Summary
* what is load?
* more pods or more nodes?
* autoscaling/v1 - cpu only
* autoscaling/v2 - memory and custom metrics

# Horizontal Pod Autoscaler
* pods
* increases replica count in deployment
* scale out
* 1:1 with deployment
* must create pods with resource requests <<
* targetCPUUtilizationPercentage: percentage of resources _asked for_
* only knows WHEN, not HOW to scale
* works on actual values
* every 30 seconds
* versions:
  * v1: CPU ony
  * v2: CPU, memory, custom metrics (need prometheus) 

# Cluster Autoscaler
* pools of like nodes - tied into cloud's Kubernetes service
* max/min
* must configure pods with resource requsts <<
* works on requested values
* checks every 10 seconds (throttling)
* performance on really big clusters with node affinity rules a problem
* affinities
  * node affinity - propery of pod
  * taint - property of node
  * toleration - property of pod


# Vertical Pod Autoscaler
* changing resources for pods
