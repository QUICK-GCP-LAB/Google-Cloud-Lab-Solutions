# Get Started with Pub/Sub: Challenge Lab || [ARC113](https://www.cloudskillsboost.google/focuses/63246?parent=catalog) ||

## Solution [here](https://youtu.be/qtj4QyRnuzU)

```
export LOCATION=
export MSG_BODY=''
```
### Task 1. Set up Cloud Pub/Sub

```
gcloud pubsub topics create $DEVSHELL_PROJECT_ID-cron-topic

gcloud pubsub subscriptions create $DEVSHELL_PROJECT_ID-cron-sub --topic $DEVSHELL_PROJECT_ID-cron-topic
```
### Task 2. Create a Cloud Scheduler job
```
gcloud services enable cloudscheduler.googleapis.com

gcloud scheduler jobs create pubsub $DEVSHELL_PROJECT_ID-cron-scheduler-job --schedule="* * * * *" --location $LOCATION --topic $DEVSHELL_PROJECT_ID-cron-topic --message-body="$MSG_BODY"
```
### Task 3. Verify the results in Cloud Pub/Sub
```
gcloud pubsub subscriptions pull $DEVSHELL_PROJECT_ID-cron-sub --limit 5
```

### Congratulations 🎉 for completing the Challenge Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/QuickGcpLab) & [Discussion group](https://t.me/QuickGcpLabChats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)
