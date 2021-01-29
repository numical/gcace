# Instance Groups
* unmanaged
  * load balancing only
  * cannot be multi-zone
  * will not delete instances
* managed
  * cool down period - time before utilisation monitored
  * stabilisation period - calculate size based on peak load in the this last period
  * scale-in controls
    * maximum reduction (number of instances that can be dropped within time window)
    * trailing time window - the time for this 
* reliable automation

# Automation
* SRE is mindset
* elasticity