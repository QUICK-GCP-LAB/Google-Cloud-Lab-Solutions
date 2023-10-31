# Ensure Access & Identity in Google Cloud: Challenge Lab || [GSP342](https://www.cloudskillsboost.google/focuses/14572?parent=catalog) ||

## Solution [here]()

```
export CUSTOM_SECURITY=
```
```
export SVC_ACC=
```
```
export CLUSTER=
```
```
export ZONE=
```
### Task 1. Create a custom security role.


```
nano role-definition.yaml
```
```
title: "[Custom Securiy Role]"
description: "SUBSCRIBE QUICK GCP LAB"
stage: "ALPHA"
includedPermissions:
  - storage.buckets.get
  - storage.objects.get
  - storage.objects.list
  - storage.objects.update
  - storage.objects.create
```
```
gcloud iam roles $CUSTOM_SECURITY --project $DEVSHELL_PROJECT_ID \
--file role-definition.yaml
```

### Task 2. Create a service account. & Task 3. Bind a custom security role to a service account.

* *Navigate to IAM & Admin* -> `Service Accounts` -> `CREATE SERVICE ACCOUNT`.
* *Service account name* : `orca-private-cluster-sa` , 
* *then click* `create and add roles`.

* *Roles*:
1. *orca_storage_update*
2. *Monitoring Viewer*
3. *Monitoring Metric Writer*
4. *Logs Writer*

* `Click CONTINUE` -> `DONE`

### Task 4. Create and configure a new Kubernetes Engine private cluster

```
gcloud container clusters create $CLUSTER --num-nodes 1 --master-ipv4-cidr=172.16.0.64/28 --network orca-build-vpc --subnetwork orca-build-subnet --enable-master-authorized-networks --master-authorized-networks 192.168.10.2/32 --enable-ip-alias --enable-private-nodes --enable-private-endpoint --service-account $SVC_ACC@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --zone $ZONE
```

### Task 5. Deploy an application to a private Kubernetes Engine cluster.

```
sudo apt-get install google-cloud-sdk-gke-gcloud-auth-plugin
echo "export USE_GKE_GCLOUD_AUTH_PLUGIN=True" >> ~/.bashrc
source ~/.bashrc
gcloud container clusters get-credentials <your cluster name> --internal-ip --project=<project ID> --zone <cluster zone>
kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
```
### Congratulations 🎉 for completing the Challenge Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/QuickGcpLab) & [Discussion group](https://t.me/QuickGcpLabChats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)
