# Use APIs to Work with Cloud Storage: Challenge Lab || [ARC125](https://www.cloudskillsboost.google/focuses/65991?parent=catalog) ||

## Solution [here]()

### Task 1. Create two Cloud Storage buckets

```
nano values.json
```
1. Open the [OAuth 2.0 playground](https://developers.google.com/oauthplayground/) in a new tab. This is a service that allows you to generate OAuth tokens with ease.

2. Scroll down and select *Cloud Storage API V1*.

3. Then select the `https://www.googleapis.com/auth/devstorage.full_control` scope.

4. Click on the blue box that says *Authorize APIs*. This opens the Google Sign-in page.

5. Select your username and then click *Allow* when prompted for permissions.

`OAuth 2.0 Playground opens, notice that Step 2 has an authorization code generated.`

6. Click on `Exchange authorization code for tokens`. If you get moved to Step 3, click on the Step 2 panel.

7. `Copy` the access token to use in the next step.

```
export OAUTH2_TOKEN=
```
```
export PROJECT_ID=$(gcloud config get-value project)

curl -X POST --data-binary @values.json \
    -H "Authorization: Bearer $OAUTH2_TOKEN" \
    -H "Content-Type: application/json" \
    "https://www.googleapis.com/storage/v1/b?project=$PROJECT_ID"
```
```
nano values.json
```
```
curl -X POST --data-binary @values.json \
    -H "Authorization: Bearer $OAUTH2_TOKEN" \
    -H "Content-Type: application/json" \
    "https://www.googleapis.com/storage/v1/b?project=$PROJECT_ID"
```

### Task 2. Upload an image file to a Cloud Storage Bucket

1. For this task, save this [image](https://cdn.qwiklabs.com/amN7kZDhflOmMUaM3tiFSjyw5yfXIqOxtrpslYJS2Kg%3D) to your computer and give it a name `demo-image`.

```
realpath demo-image
```
```
export OBJECT=
```
```
export BUCKET_NAME_1=$(gcloud config get-value project)-bucket-1

export BUCKET_NAME_2=$(gcloud config get-value project)-bucket-2
```
```
curl -X POST --data-binary @$OBJECT \
    -H "Authorization: Bearer $OAUTH2_TOKEN" \
    -H "Content-Type: image/png" \
    "https://www.googleapis.com/upload/storage/v1/b/$BUCKET_NAME_1/o?uploadType=media&name=demo-image"
```

### Task 3. Copy a file to another bucket

```
curl -X POST \
  -H "Authorization: Bearer $OAUTH2_TOKEN" \
  -H "Content-Length: 0" \
  "https://storage.googleapis.com/storage/v1/b/$BUCKET_NAME_1/o/demo-image/rewriteTo/b/$BUCKET_NAME_2/o/demo-image"
```

### Task 4. Make an object (file) publicly accessible

```
nano quickgcplab.json
```
```
curl -X POST --data-binary @quickgcplab.json \
  -H "Authorization: Bearer $OAUTH2_TOKEN" \
  -H "Content-Type: application/json" \
  "https://storage.googleapis.com/storage/v1/b/$BUCKET_NAME_1/o/demo-image/acl"
```

### Task 5. Delete the object file and a Cloud Storage bucket (Bucket 1)

```
curl -X DELETE \
  -H "Authorization: Bearer $OAUTH2_TOKEN" \
  "https://storage.googleapis.com/storage/v1/b/$BUCKET_NAME_1/o/demo-image"

curl -X DELETE -H "Authorization: Bearer $OAUTH2_TOKEN" \
  "https://storage.googleapis.com/storage/v1/b/$BUCKET_NAME_1"
  ```

  ### Congratulations 🎉 for completing the Challenge Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/QuickGcpLab) & [Discussion group](https://t.me/QuickGcpLabChats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)
