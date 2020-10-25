#Requirement
* Brand new project
* GCE instance that runs provided script
* system logs available in stackdriver logs
* new gcs bucket for resulting log files
* log file appears in new bucket after instance finishes starting up
* no need to SSH onto instance

## Script
```
#! /bin/bash

#
# Echo commands as they are run, to make debugging easier.
# GCE startup script output shows up in "/var/log/syslog" .
#
set -x


#
# Stop apt-get calls from trying to bring up UI.
#
export DEBIAN_FRONTEND=noninteractive


#
# Make sure installed packages are up to date with all security patches.
#
apt-get -yq update
apt-get -yq upgrade


#
# Install Google's Stackdriver logging agent, as per
# https://cloud.google.com/logging/docs/agent/installation
#
curl -sSO https://dl.google.com/cloudagents/install-logging-agent.sh
bash install-logging-agent.sh


#
# Install and run the "stress" tool to max the CPU load for a while.
#
apt-get -yq install stress
stress -c 8 -t 120


#
# Report that we're done.
#

# Metadata should be set in the "lab-logs-bucket" attribute using the "gs://mybucketname/" format.
log_bucket_metadata_name=lab-logs-bucket
log_bucket_metadata_url="http://metadata.google.internal/computeMetadata/v1/instance/attributes/${log_bucket_metadata_name}"
worker_log_bucket=$(curl -H "Metadata-Flavor: Google" "${log_bucket_metadata_url}")

# We write a file named after this machine.
worker_log_file="machine-$(hostname)-finished.txt"
echo "Phew!  Work completed at $(date)" >"${worker_log_file}"

# And we copy that file to the bucket specified in the metadata.
echo "Copying the log file to the bucket..."
gsutil cp "${worker_log_file}" "${worker_log_bucket}"

```

## Lessons
* instance config:
  * script
  * bucket name
  * scopes
  * service account
* metadata service on host machine
  * script
  * bucket name
  * ACCESS TOKEN - minimal of scopes and service account

## Notes
* gs://chapter-8-challenge-bucket

### CLI
```
gloud projects create chpater-8-callenge-auto --enable-cloud-apis 
gcloud alpha billing projects link chpater-8-challenge-auto --billing-account 01EBDB-D66A7B-28C6EC
gsutil mb gs://chapter-8-challenge-bucket-auto
gcloud compute instances create chapter-8-challenge-vm-auto --machine-type=f1-micro --metadata-from-file=startup-script=chapter8-startup --metadata=lab-logs-bucket=gs://chapter-8-challenge-bucket-auto --scopes=default,storage-rw --zone=us-central1-a
```
and then
```
gcloud projects delete chpater-8-challenge-auto
```

### Script
```
gloud projects create chapter-8-challenge-script --enable-cloud-apis 
gcloud alpha billing projects link chapter-8-challenge-script --billing-account 01EBDB-D66A7B-28C6EC
gsutil mb -p chapter-8-challenge-script gs://chapter-8-challenge-script-bucket 
gcloud compute instances create chapter-8-challenge-script-vm --machine-type=f1-micro --metadata-from-file=startup-script=chapter8-startup --metadata=lab-logs-bucket=gs://chapter-8-challenge-script-bucket --project=chapter-8-challenge-script --scopes=default,storage-rw --zone=us-central1-a
```


# Example Questions
## Tactics
* Understand
  * what does everything mean
  * the kicker
* Eliminate
* Evaluate
* Choose
* Validate
## Lessons
* don't guess on stuff you don't know!

        