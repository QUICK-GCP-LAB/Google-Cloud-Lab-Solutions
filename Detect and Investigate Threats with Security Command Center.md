# Detect and Investigate Threats with Security Command Center

## Solution [here]()

1. In the Google Cloud Console open the navigation menu and select `IAM & Admin > Audit Logs`.

2. In the list of services find `Cloud Resource Manager API` and click the `checkbox` next to it.

3. On the right side of the tab, find the configuration frame: `Cloud Resource Manager API - Log Types`.

4. Select the `Admin Read` check box and click `Save`.

```
export ZONE=
```
```
export PROJECT_NUMBER=$(gcloud projects describe $DEVSHELL_PROJECT_ID --format="value(projectNumber)")
```

### Task 1. Initiate and mitigate a threat with Event Threat Detection
```
gcloud services enable securitycenter.googleapis.com --project=$DEVSHELL_PROJECT_ID

sleep 15

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
--member=user:demouser1@gmail.com --role=roles/bigquery.admin

gcloud projects remove-iam-policy-binding $DEVSHELL_PROJECT_ID \
--member=user:demouser1@gmail.com --role=roles/bigquery.admin
```
### Task 2. Configure a cloud environment to detect threats

```
gcloud compute instances create instance-1 --project=$DEVSHELL_PROJECT_ID --zone=$ZONE --machine-type=e2-medium --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=default --metadata=enable-oslogin=true --maintenance-policy=MIGRATE --provisioning-model=STANDARD --scopes=https://www.googleapis.com/auth/cloud-platform --create-disk=auto-delete=yes,boot=yes,device-name=instance-1,image=projects/debian-cloud/global/images/debian-11-bullseye-v20230912,mode=rw,size=10,type=projects/$DEVSHELL_PROJECT_ID/zones/$ZONE/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --labels=goog-ec-src=vm_add-gcloud --reservation-affinity=any
```
### Task 3. Manage SCC findings with Event Threat Detection

```
gcloud dns --project=$DEVSHELL_PROJECT_ID policies create dns-test-policy --description="SUBSCRIBE TO QUICK GCP LAB" --networks="default" --alternative-name-servers="" --private-alternative-name-servers="" --no-enable-inbound-forwarding --enable-logging

gcloud compute ssh --zone "$ZONE" "instance-1" --tunnel-through-iap --project "$DEVSHELL_PROJECT_ID" --quiet --command "gcloud projects get-iam-policy \$(gcloud config get project) && curl etd-malware-trigger.goog"
```
* Check The Score For Task 2 Do Not Move Forward Until You Get Score & Green Check.

```
gcloud compute instances delete instance-1 --zone=$ZONE --quiet
```

### Task 4. Build an environment for detecting container threats

```
gcloud compute instances create attacker-instance \
--scopes=cloud-platform  \
--zone=$ZONE \
--machine-type=e2-medium  \
--image-family=ubuntu-2004-lts \
--image-project=ubuntu-os-cloud \
--no-address


gcloud compute networks subnets update default \
--region="${ZONE%-*}" \
--enable-private-ip-google-access
```

* Open the navigation menu and select `Compute Engine > VM Instances`.

* Once the instance is created, click on the `SSH` button to access the `attacker-instance`.

* Paste The Follwing Commands in `attacker-instance` SSH

```
export ZONE=
```
```
sudo snap remove google-cloud-cli

curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-438.0.0-linux-x86_64.tar.gz

tar -xf google-cloud-cli-438.0.0-linux-x86_64.tar.gz

./google-cloud-sdk/install.sh
```
```
. ~/.bashrc

gcloud components install kubectl gke-gcloud-auth-plugin --quiet

gcloud container clusters create test-cluster \
--zone "$ZONE" \
--enable-private-nodes \
--enable-private-endpoint \
--enable-ip-alias \
--num-nodes=1 \
--master-ipv4-cidr "172.16.0.0/28" \
--enable-master-authorized-networks \
--master-authorized-networks "10.128.0.0/20"
```
```
kubectl describe daemonsets container-watcher -n kube-system
```

* It will take a few minutes for an output to be generated. If you get a message similar to the following: ( *do not copy it* ).
```
Error from server (NotFound): daemonsets.apps "container-watcher" not found
```

* Wait a moment and rerun the command. After a few minutes, you should receive the following output: ( *do not copy it* ).

```
Name:           container-watcher
Selector:       container-watcher-unique-id=adbc885a,k8s-app=container-watcher
Node-Selector:  kubernetes.io/os=linux
Labels:         BUILD_BASELINE_CHANGELIST=579306457
                k8s-app=container-watcher
                ktd-version=ktd_release.watcher_20231103.01_RC00
Annotations:    deprecated.daemonset.template.generation: 1
Desired Number of Nodes Scheduled: 1
Current Number of Nodes Scheduled: 1
Number of Nodes Scheduled with Up-to-date Pods: 1
```

* After You Getting Out Put Paste This Command

```
kubectl create deployment apache-deployment \
--replicas=1 \
--image=us-central1-docker.pkg.dev/cloud-training-prod-bucket/scc-labs/ktd-test-httpd:2.4.49-vulnerable

kubectl expose deployment apache-deployment \
--name apache-test-service  \
--type NodePort \
--protocol TCP \
--port 80

NODE_IP=$(kubectl get nodes -o jsonpath={.items[0].status.addresses[0].address})
NODE_PORT=$(kubectl get service apache-test-service \
-o jsonpath={.spec.ports[0].nodePort})

gcloud compute firewall-rules create apache-test-service-fw \
--allow tcp:${NODE_PORT}

gcloud compute firewall-rules create apache-test-rvrs-cnnct-fw --allow tcp:8888
```