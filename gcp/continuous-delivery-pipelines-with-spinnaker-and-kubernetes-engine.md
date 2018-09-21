

show auht list
```console
oogle1102461_student@cloudshell:~ (qwiklabs-gcp-e3f82dd64d10f7b8)$ gcloud auth list
          Credentialed Accounts
ACTIVE  ACCOUNT
*       google1102461_student@qwiklabs.net

To set the active account, run:
    $ gcloud config set account `ACCOUNT`
```

list project
```console
google1102461_student@cloudshell:~ (qwiklabs-gcp-e3f82dd64d10f7b8)$ gcloud config list project
[core]
project = qwiklabs-gcp-e3f82dd64d10f7b8

Your active configuration is: [cloudshell-21387]
```

## set up environment

### kubernetes

set compute zone
```console
$ gcloud config set compute/zone us-central1-f
Updated property [compute/zone].
```

```console
$ gcloud container clusters create spinnaker-tutorial --machine-type=n1-standard-2 --enable-legacy-authorization
WARNING: Starting in 1.12, new clusters will have basic authentication disabled by default. Basic authentication can be enabled (or disabled) manually using the `--[no-]enable-basic-aut
h` flag.
WARNING: Starting in 1.12, new clusters will not have a client certificate issued. You can manually enable (or disable) the issuance of the client certificate using the `--[no-]issue-cl
ient-certificate` flag.
WARNING: Currently VPC-native is not the default mode during cluster creation. In the future, this will become the default mode and can be disabled using `--no-enable-ip-alias` flag. Us
e `--[no-]enable-ip-alias` flag to suppress this warning.
This will enable the autorepair feature for nodes. Please see
https://cloud.google.com/kubernetes-engine/docs/node-auto-repair for more
information on node autorepairs.
WARNING: Starting in Kubernetes v1.10, new clusters will no longer get compute-rw and storage-ro scopes added to what is specified in --scopes (though the latter will remain included in
 the default --scopes). To use these scopes, add them explicitly to --scopes. To use the new behavior, set container/new_scopes_behavior property (gcloud config set container/new_scopes
_behavior true).

Creating cluster spinnaker-tutorial...⠛

Creating cluster spinnaker-tutorial...done.
Created [https://container.googleapis.com/v1/projects/qwiklabs-gcp-e3f82dd64d10f7b8/zones/us-central1-f/clusters/spinnaker-tutorial].
To inspect the contents of your cluster, go to: https://console.cloud.google.com/kubernetes/workload_/gcloud/us-central1-f/spinnaker-tutorial?project=qwiklabs-gcp-e3f82dd64d10f7b8
kubeconfig entry generated for spinnaker-tutorial.
NAME                LOCATION       MASTER_VERSION  MASTER_IP       MACHINE_TYPE   NODE_VERSION  NUM_NODES  STATUS
spinnaker-tutorial  us-central1-f  1.9.7-gke.6     35.226.186.175  n1-standard-2  1.9.7-gke.6   3          RUNNING
```

configure identity and access management

create the service account
```console
gcloud iam service-accounts create  spinnaker-storage-account \
    --display-name spinnaker-storage-account
```    

```
$ export SA_EMAIL=$(gcloud iam service-accounts list \
    --filter="displayName:spinnaker-storage-account" \
    --format='value(email)')
```

```console
$ gcloud iam service-accounts list
NAME                                    EMAIL
App Engine default service account      qwiklabs-gcp-e3f82dd64d10f7b8@appspot.gserviceaccount.com
ql-api                                  qwiklabs-gcp-e3f82dd64d10f7b8@qwiklabs-gcp-e3f82dd64d10f7b8.iam.gserviceaccount.com
Compute Engine default service account  787646769113-compute@developer.gserviceaccount.com
spinnaker-storage-account               spinnaker-storage-account@qwiklabs-gcp-e3f82dd64d10f7b8.iam.gserviceaccount.com
```
```console
$ export PROJECT=$(gcloud info --format='value(config.project)')
```
```console
$ gcloud info --format='value(config.project)'
qwiklabs-gcp-e3f82dd64d10f7b8
```

```console
$ gcloud projects add-iam-policy-binding \
>     $PROJECT --role roles/storage.admin --member serviceAccount:$SA_EMAIL
bindings:
- members:
  - serviceAccount:service-787646769113@gae-api-prod.google.com.iam.gserviceaccount.com
  role: roles/appengineflex.serviceAgent
- members:
  - serviceAccount:service-787646769113@gcp-sa-bigquerydatatransfer.iam.gserviceaccount.com
  role: roles/bigquerydatatransfer.serviceAgent
- members:
  - serviceAccount:787646769113@cloudbuild.gserviceaccount.com
  role: roles/cloudbuild.builds.builder
- members:
  - serviceAccount:service-787646769113@gcf-admin-robot.iam.gserviceaccount.com
  role: roles/cloudfunctions.serviceAgent
- members:
  - serviceAccount:service-787646769113@gcp-sa-cloudiot.iam.gserviceaccount.com
  role: roles/cloudiot.serviceAgent
- members:
  - serviceAccount:service-787646769113@cloudcomposer-accounts.iam.gserviceaccount.com
  role: roles/composer.serviceAgent
- members:
  - serviceAccount:service-787646769113@compute-system.iam.gserviceaccount.com
  role: roles/compute.serviceAgent
- members:
  - serviceAccount:service-787646769113@container-engine-robot.iam.gserviceaccount.com
  role: roles/container.serviceAgent
- members:
  - serviceAccount:service-787646769113@dataflow-service-producer-prod.iam.gserviceaccount.com
  role: roles/dataflow.serviceAgent
- members:
  - serviceAccount:service-787646769113@dataproc-accounts.iam.gserviceaccount.com
  role: roles/dataproc.serviceAgent
- members:
  - serviceAccount:service-787646769113@dlp-api.iam.gserviceaccount.com
  role: roles/dlp.serviceAgent
- members:
  - serviceAccount:787646769113-compute@developer.gserviceaccount.com
  - serviceAccount:787646769113@cloudservices.gserviceaccount.com
  - serviceAccount:qwiklabs-gcp-e3f82dd64d10f7b8@appspot.gserviceaccount.com
  - serviceAccount:qwiklabs-gcp-e3f82dd64d10f7b8@qwiklabs-gcp-e3f82dd64d10f7b8.iam.gserviceaccount.com
  - serviceAccount:service-787646769113@containerregistry.iam.gserviceaccount.com
  - user:google1102461_student@qwiklabs.net
  role: roles/editor
- members:
  - serviceAccount:service-787646769113@firebase-rules.iam.gserviceaccount.com
  role: roles/firebaserules.system
- members:
  - serviceAccount:service-787646769113@genomics-api.google.com.iam.gserviceaccount.com
  role: roles/genomics.serviceAgent
- members:
  - serviceAccount:service-787646769113@cloud-ml.google.com.iam.gserviceaccount.com
  role: roles/ml.serviceAgent
- members:
  - serviceAccount:936076353769-dcb7hgk8cpl26aetfq99c7min7o6qfrr@developer.gserviceaccount.com
  - serviceAccount:qwiklabs-gcp-e3f82dd64d10f7b8@qwiklabs-gcp-e3f82dd64d10f7b8.iam.gserviceaccount.com
  - user:google1102461_student@qwiklabs.net
  role: roles/owner
- members:
  - serviceAccount:service-787646769113@sourcerepo-service-accounts.iam.gserviceaccount.com
  role: roles/sourcerepo.serviceAgent
- members:
  - serviceAccount:spinnaker-storage-account@qwiklabs-gcp-e3f82dd64d10f7b8.iam.gserviceaccount.com
  role: roles/storage.admin
etag: BwV2Xr5hWi4=
version: 1
```

```console
$ gcloud iam service-accounts keys create spinnaker-sa.json \
>      --iam-account $SA_EMAIL
created key [4336a7c5ef28d47b29d8c669f61fca8b8216b906] of type [json] as [spinnaker-sa.json] for [spinnaker-storage-account@qwiklabs-gcp-e3f82dd64d10f7b8.iam.gserviceaccount.com]
```

## deploying spinnaker using helm

```console
$ wget https://storage.googleapis.com/kubernetes-helm/helm-v2.5.0-linux-amd64.tar.gz
$ tar zxfv helm-v2.5.0-linux-amd64.tar.gz
linux-amd64/
linux-amd64/helm
linux-amd64/LICENSE
linux-amd64/README.md
$ cp linux-amd64/helm .
```

```console
$ ./helm init
Creating /home/google1102461_student/.helm
Creating /home/google1102461_student/.helm/repository
Creating /home/google1102461_student/.helm/repository/cache
Creating /home/google1102461_student/.helm/repository/local
Creating /home/google1102461_student/.helm/plugins
Creating /home/google1102461_student/.helm/starters
Creating /home/google1102461_student/.helm/cache/archive
Creating /home/google1102461_student/.helm/repository/repositories.yaml
$HELM_HOME has been configured at /home/google1102461_student/.helm.

Tiller (the helm server side component) has been installed into your Kubernetes Cluster.
Happy Helming!
```
```console
$ ./helm repo update
Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈
```

```console
$ ./helm version
Client: &version.Version{SemVer:"v2.5.0", GitCommit:"012cb0ac1a1b2f888144ef5a67b8dab6c2d45be6", GitTreeState:"clean"}
Server: &version.Version{SemVer:"v2.5.0", GitCommit:"012cb0ac1a1b2f888144ef5a67b8dab6c2d45be6", GitTreeState:"clean"}
```

### Configure Spinnaker

```console
$ export PROJECT=$(gcloud info \
>     --format='value(config.project)')
```
```console
$ gcloud info --format='value(config.project)'
qwiklabs-gcp-e3f82dd64d10f7b8
```

```console
$ export BUCKET=$PROJECT-spinnaker-config
```

```console
$ gsutil mb -c regional -l us-central1 gs://$BUCKET
Creating gs://qwiklabs-gcp-e3f82dd64d10f7b8-spinnaker-config/...
```

```console
export SA_JSON=$(cat spinnaker-sa.json)
export PROJECT=$(gcloud info --format='value(config.project)')
export BUCKET=$PROJECT-spinnaker-config
cat > spinnaker-config.yaml <<EOF
storageBucket: $BUCKET
gcs:
  enabled: true
  project: $PROJECT
  jsonKey: '$SA_JSON'

# Disable minio the default
minio:
  enabled: false

# Configure your Docker registries here
accounts:
- name: gcr
  address: https://gcr.io
  username: _json_key
  password: '$SA_JSON'
  email: 1234@5678.com
EOF
```

### deploy the spinnaker chart
