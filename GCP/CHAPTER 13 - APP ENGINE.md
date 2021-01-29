# Google App Engine
* original google cloud service
  
# CodeLabs
* https://codelabs.developers.google.com/?cat=cloud
* GAE Standard & Flexible

## Spring Boot on App Engine
```bash
gcloud config set project elite-crossbar-298315
```

## Node ON App Engine
```bash
gcloud projects create <project-name> --set-as-default
gcloud beta billing accounts list
gcloud alpha billing projects link <project-name> --billing-account <billing-account-id>
gcloud app create --project=<project-name> --region=europe-west
git clone https://github.com/GoogleCloudPlatform/nodejs-docs-samples
cd nodejs-docs-samples/appengine/hello-world/standard
npm install
gcloud app deploy
gcloud app browse

// then later
gcloud projects delete <project-name>
```
  
# QwikLabs
* https://google.qwiklabs.com/catalog?price%5B%5D=free&per_page=50
* GAE Standard only

# Other Links
* https://cloud.google.com/appengine/docs/standard/nodejs/tutorials