# Stackdriver
* operations suite
* dynamic discovery in GCP
* intelligent defaults
* open source agents / interactions
* collaboration with third party

# Monitoring
* the base of SRE
* workspace is root entity - a single pane of glass
* holds
  * monitoring data
  * config info
* hosting project (name's the same)
* any number of other projects (inc. AWS connector)
* alerting policy
  * if metric
  * condition
  * threshold
  * for (duration)
* uptime check
* some metrics in VM without monitoring agent
  * uptime
  * cpu 
  * network
  * some disc
* install via curl'd script
* custom metrics

# Logging
* API to write to logs (?)
* 30 days only, so export
* install logging agent on VM - again curl a script

# Error Reporting


# Trace
* latency data for
* app engine
* http(s) load balancers
* applications instrumented with cloud trace sdk's


# Debugger
* < 10 ms impact
* inject into service withut stopping it