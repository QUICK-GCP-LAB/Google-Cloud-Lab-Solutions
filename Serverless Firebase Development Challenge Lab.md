# Serverless Firebase Development: Challenge Lab || [GSP344](https://www.cloudskillsboost.google/focuses/14677?parent=catalog) ||

## Solution [here]()

#### Assign Veriables & Region

```
PROJECT_ID=
CLOUD_RUN_SERVICE_1=
CLOUD_RUN_SERVICE_2=
CLOUD_RUN_SERVICE_3=
gcloud config set run/region
```
```
git clone https://github.com/rosera/pet-theory.git
```

### Task 1. Create a Firestore database

1. In the Cloud Console, `Search Bar` Type `Firestore` and select.

2. Click the Select `Native Mode` button.

3. In the Select a location dropdown, Select `Nam5` `(United States)` and then click `Create Database`.

### Task 2. Populate the Database

```
cd pet-theory/lab06/firebase-import-csv/solution
npm install
node index.js netflix_titles_original.csv
```

### Task 3. Create a REST API

```
cd ~/pet-theory/lab06/firebase-rest-api/solution-01
npm install
gcloud builds submit --tag gcr.io/$PROJECT_ID/rest-api:0.1
gcloud beta run deploy $CLOUD_RUN_SERVICE_1 --image gcr.io/$PROJECT_ID/rest-api:0.1 --allow-unauthenticated
```
```
SERVICE_URL=
```
```
curl -X GET $SERVICE_URL
```

### Task 4. Firestore API access

```
cd ~/pet-theory/lab06/firebase-rest-api/solution-02
npm install
gcloud builds submit --tag gcr.io/$PROJECT_ID/rest-api:0.2
gcloud beta run deploy $CLOUD_RUN_SERVICE_1 --image gcr.io/$PROJECT_ID/rest-api:0.2 --allow-unauthenticated
curl -X GET $SERVICE_URL/2019
```

### Task 5. Deploy the Staging Frontend

```
cd ~/pet-theory/lab06/firebase-frontend/public
nano app.js
```
* *`Follow Video`* *`Instruction`*
```
npm install
cd ~/pet-theory/lab06/firebase-frontend
gcloud builds submit --tag gcr.io/$PROJECT_ID/frontend-staging:0.1
gcloud beta run deploy $CLOUD_RUN_SERVICE_2 --image gcr.io/$PROJECT_ID/frontend-staging:0.1 --allow-unauthenticated
```

### Task 6. Deploy the Production Frontend

```
gcloud builds submit --tag gcr.io/$PROJECT_ID/frontend-production:0.1
gcloud beta run deploy $CLOUD_RUN_SERVICE_3 --image gcr.io/$GOOGLE_CLOUD_PROJECT/frontend-production:0.1 --allow-unauthenticated
```

### Congratulations 🎉 for completing the Challenge Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/QuickGcpLab) & [Discussion group](https://t.me/QuickGcpLabChats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)
