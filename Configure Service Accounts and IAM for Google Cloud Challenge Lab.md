# Configure Service Accounts and IAM for Google Cloud: Challenge Lab || [ARC134](https://www.cloudskillsboost.google/focuses/67219?parent=catalog) ||

## Solution [here]()

```
gcloud auth login
```
```
export PROJECT_ID=$(gcloud config get-value project)
```
```
gcloud config set compute/region [REGION]
```
```
gcloud config set compute/zone [ZONE]
```

## Task 1. Create a service account using the gcloud CLI

```
gcloud iam service-accounts create devops --display-name devops
```
## Task 2. Grant IAM permissions to a service account using the gcloud CLI

```
SA=$(gcloud iam service-accounts list --format="value(email)" --filter "displayName=devops")

gcloud projects add-iam-policy-binding $PROJECT_ID --member serviceAccount:$SA --role=roles/iam.serviceAccountUser

gcloud projects add-iam-policy-binding $PROJECT_ID --member serviceAccount:$SA --role=roles/compute.instanceAdmin
```
## Task 3. Create a compute instance with a service account attached using gcloud

```
gcloud compute instances create vm-2 --machine-type=e2-standard-2 --service-account $SA --scopes "https://www.googleapis.com/auth/compute"
```
## Task 4. Create a custom role using a YAML file

```
cat > role-definition.yaml <<EOF
title: Custom Role
description: Custom role with cloudsql.instances.connect and cloudsql.instances.get permissions
includedPermissions:
- cloudsql.instances.connect
- cloudsql.instances.get
EOF
```
```
gcloud iam roles create customRole --project=$PROJECT_ID --file=role-definition.yaml
```
## Task 5. Use the client libraries to access BigQuery from a service account

```
gcloud iam service-accounts create bigquery-qwiklab --display-name bigquery-qwiklab

SA=$(gcloud iam service-accounts list --format="value(email)" --filter "displayName=bigquery-qwiklab")

gcloud projects add-iam-policy-binding $PROJECT_ID --member serviceAccount:$SA --role=roles/bigquery.dataViewer

gcloud projects add-iam-policy-binding $PROJECT_ID --member serviceAccount:$SA --role=roles/bigquery.user

gcloud compute instances create bigquery-instance --machine-type=e2-medium --service-account $SA --scopes "https://www.googleapis.com/auth/compute"
```
##### SSH into the `bigquery-instance` and install dependencies; use the following code to create a Python file: 

```
export PROJECT_ID=$(gcloud config get-value project)
```
```
sudo apt-get update

sudo apt-get install -y git python3-pip

pip3 install --upgrade pip

pip3 install google-cloud-bigquery

pip3 install pyarrow

pip3 install pandas

pip3 install db-dtypes
```
```
echo "
from google.auth import compute_engine
from google.cloud import bigquery
credentials = compute_engine.Credentials(
    service_account_email='bigquery-qwiklab@$PROJECT_ID.iam.gserviceaccount.com')
query = '''
SELECT name, SUM(number) as total_people
FROM "bigquery-public-data.usa_names.usa_1910_2013"
WHERE state = 'TX'
GROUP BY name, state
ORDER BY total_people DESC
LIMIT 20
'''
client = bigquery.Client(
    project='$PROJECT_ID',
    credentials=credentials)
print(client.query(query).to_dataframe())
" > query.py
```
```
pip3 install --upgrade pip

pip3 install google-cloud-bigquery

pip3 install pyarrow

pip3 install pandas

pip3 install db-dtypes

python3 query.py
```

### Congratulations 🎉 for completing the Challenge Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/QuickGcpLab) & [Discussion group](https://t.me/QuickGcpLabChats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)