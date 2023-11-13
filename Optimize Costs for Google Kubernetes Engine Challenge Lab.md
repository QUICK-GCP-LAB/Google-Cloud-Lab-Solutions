# Optimize Costs for Google Kubernetes Engine: Challenge Lab || [GSP343](https://www.cloudskillsboost.google/focuses/16327?parent=catalog) ||

## Solution [here]()

 ```
export ZONE=
 ```
  ```
export CLUSTER=
 ```
```
export POOL=
 ```
### Task 1. Create our cluster and deploy our app
 ```
gcloud container clusters create $CLUSTER \
   --project=${DEVSHELL_PROJECT_ID} --zone $ZONE \
    --machine-type=e2-standard-2 --num-nodes=2
 ```
  ```
kubectl create namespace dev
kubectl create namespace prod
 ```
  ```
kubectl config set-context --current --namespace dev
 ```
  ```
git clone https://github.com/GoogleCloudPlatform/microservices-demo.git
cd microservices-demo
kubectl apply -f ./release/kubernetes-manifests.yaml --namespace dev
 ```
  ```
kubectl get svc -w --namespace dev
 ```

### Task 2. Migrate to an optimized node pool

 ```
gcloud container node-pools create $POOL \
   --cluster $CLUSTER \
   --machine-type=custom-2-3584 \
   --num-nodes=2 \
   --zone $ZONE
```
```
for node in $(kubectl get nodes -l cloud.google.com/gke-nodepool=default-pool -o=name); do
   kubectl cordon "$node";
done
   
for node in $(kubectl get nodes -l cloud.google.com/gke-nodepool=default-pool -o=name); do
   kubectl drain --force --ignore-daemonsets --delete-local-data --grace-period=10 "$node";
done
```
```
gcloud container node-pools delete default-pool \
   --cluster $CLUSTER --zone $ZONE
```

### Task 3. Apply a frontend update

```
kubectl create poddisruptionbudget onlineboutique-frontend-pdb \
--selector app=frontend --min-available 1  --namespace dev
```
```
KUBE_EDITOR="nano" kubectl edit deployment/frontend --namespace dev
```
#### Change the following in the configuration:

* *image: gcr.io/google-samples/microservices-demo/frontend:v2.1  
        imagePullPolicy: Always*

### Task 4. Autoscale from estimated traffic

```
kubectl autoscale deployment frontend --cpu-percent=50 \
   --min=1 --max=[Max Replicas] --namespace dev
```
```
kubectl get hpa --namespace dev

gcloud beta container clusters update $CLUSTER \
   --enable-autoscaling --min-nodes 1 --max-nodes 6 --zone $ZONE
```

### Congratulations 🎉 for completing the Challenge Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/QuickGcpLab) & [Discussion group](https://t.me/QuickGcpLabChats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)