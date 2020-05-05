Spinnaker Playground
===

### Install halyard

Require openjdk8

```
curl -O https://raw.githubusercontent.com/spinnaker/halyard/master/install/debian/InstallHalyard.sh
sudo bash InstallHalyard.sh
```

### Config Halyard

```
hal config provider kubernetes enable

VERSION=1.20.0
hal config version edit --version $VERSION
hal config provider kubernetes account add my-k8s-account \
    --context $(kubectl config current-context)
ACCOUNT=my-k8s-account
hal config deploy edit --type distributed --account-name $ACCOUNT

PROJECT=gke-playground-0423
BUCKET_LOCATION=asia
SERVICE_ACCOUNT_DEST=/Users/david/workspace/credentials/gke-playground-0423-aacf6a39cc3f.json
hal config storage gcs edit --project $PROJECT \
    --bucket-location $BUCKET_LOCATION \
    --json-path $SERVICE_ACCOUNT_DEST
hal config storage edit --type gcs

sudo hal deploy apply
```
