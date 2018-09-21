

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
