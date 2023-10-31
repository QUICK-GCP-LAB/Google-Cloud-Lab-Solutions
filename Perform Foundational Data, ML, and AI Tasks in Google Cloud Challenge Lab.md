# Perform Foundational Data, ML, and AI Tasks in Google Cloud: Challenge Lab || [GSP323](https://www.cloudskillsboost.google/focuses/11044?parent=catalog) ||

## Solution [here](https://youtu.be/q_PxFoQwMM8)

## Task  1 : Run a simple Dataflow job

```
bq mk REPLACE_HERE
```
```
gsutil mb gs://REPLACE_HERE
```
```
gsutil cp gs://cloud-training/gsp323/lab.csv  .
gsutil cp gs://cloud-training/gsp323/lab.schema .
cat lab.schema
```

## Task  2 : Run a simple Dataproc job

### `For Task 2 Follow Video`

```
export API_KEY=
```
```
export TASK_3_BUCKET=
```
```
export TASK_4_BUCKET=
```

## Task 3: Use the Google Cloud Speech API

```
gcloud iam service-accounts create Awesome \
  --display-name "my natural language service account"

gcloud iam service-accounts keys create ~/key.json \
  --iam-account Awesome@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com

export GOOGLE_APPLICATION_CREDENTIALS="/home/$USER/key.json"

gcloud auth activate-service-account Awesome@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com --key-file=$GOOGLE_APPLICATION_CREDENTIALS

gcloud ml language analyze-entities --content="Old Norse texts portray Odin as one-eyed and long-bearded, frequently wielding a spear named Gungnir and wearing a cloak and a broad hat." > result.json
```
```
gcloud auth login --no-launch-browser
```

## Task 4: Use the Cloud Natural Language API

```
gsutil cp result.json $TASK_4_BUCKET
```
```
cat > request.json <<EOF 
{
  "config": {
      "encoding":"FLAC",
      "languageCode": "en-US"
  },
  "audio": {
      "uri":"gs://cloud-training/gsp323/task3.flac"
  }
}
EOF
```
```
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > result.json

gsutil cp result.json $TASK_3_BUCKET
```
```
gcloud iam service-accounts create quick-gcp-lab

gcloud iam service-accounts keys create key.json --iam-account quick-gcp-lab@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com

gcloud auth activate-service-account --key-file key.json

export ACCESS_TOKEN=$(gcloud auth print-access-token)
```
```
cat > request.json <<EOF 
{
   "inputUri":"gs://spls/gsp154/video/train.mp4",
   "features": [
       "TEXT_DETECTION"
   ]
}
EOF
```
```
curl -s -H 'Content-Type: application/json' \
    -H "Authorization: Bearer $ACCESS_TOKEN" \
    'https://videointelligence.googleapis.com/v1/videos:annotate' \
    -d @request.json
```
```
curl -s -H 'Content-Type: application/json' -H "Authorization: Bearer $ACCESS_TOKEN" 'https://videointelligence.googleapis.com/v1/operations/OPERATION_FROM_PREVIOUS_REQUEST' > result1.json
```

### Congratulations 🎉 for completing the Challenge Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/QuickGcpLab) & [Discussion group](https://t.me/QuickGcpLabChats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)
