# Cloud Speech API 3 Ways: Challenge Lab || [ARC132](https://www.cloudskillsboost.google/focuses/67215?parent=catalog) ||

## Solution [here](https://youtu.be/uPtFVDPtW1o)

### Task 1: Create an API key
 
1. *To create an API key, on the `Navigation menu` click `APIs & services` > `Credentials`.*

2. *Click `Create credentials` and select `API key`.*

3. *`Copy` and record the key you just generated to use later in this lab.*

4. *Click Close.*

### Assign Veriables

```
export API_KEY=""

task_2_file_name=""
 
task_3_request_file=""
 
task_3_response_file=""
 
task_4_sentence=""
 
task_4_file=""
 
task_5_sentence=""
 
task_5_file=""

audio_uri="gs://cloud-samples-data/speech/corbeau_renard.flac"

export PROJECT_ID=$(gcloud config get-value project)
 ```

### Task 2. Create synthetic speech from text using the Text-to-Speech API


 ```
source venv/bin/activate
 ```
 ```
cat > synthesize-text.json <<EOF
 
{
'input':{
    'text':'Cloud Text-to-Speech API allows developers to include
       natural-sounding, synthetic human speech as playable audio in
       their applications. The Text-to-Speech API converts text or
       Speech Synthesis Markup Language (SSML) input into audio data
       like MP3 or LINEAR16 (the encoding used in WAV files).'
},
'voice':{
    'languageCode':'en-gb',
    'name':'en-GB-Standard-A',
    'ssmlGender':'FEMALE'
},
'audioConfig':{
    'audioEncoding':'MP3'
}
}
 
EOF
 ```
 ```
curl -H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
-H "Content-Type: application/json; charset=utf-8" \
-d @synthesize-text.json "https://texttospeech.googleapis.com/v1/text:synthesize" \
> $task_2_file_name
 ```
 
 ### Task 3. Perform speech to text transcription with the Cloud Speech API

```
cat > "$task_3_request_file" <<EOF
{
"config": {
"encoding": "FLAC",
"sampleRateHertz": 44100,
"languageCode": "fr-FR"
},
"audio": {
"uri": "$audio_uri"
}
}
EOF
 ```

```
curl -s -X POST -H "Content-Type: application/json" \
--data-binary @"$task_3_request_file" \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" \
-o "$task_3_response_file"
 ```
 ### Task 4. Translate text with the Cloud Translation API

 ```
response=$(curl -s -X POST \
-H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
-H "Content-Type: application/json; charset=utf-8" \
-d "{\"q\": \"$task_4_sentence\"}" \
"https://translation.googleapis.com/language/translate/v2?key=${API_KEY}&source=ja&target=en")
echo "$response" > "$task_4_file"
 ```
 ### Task 5. Detect a language with the Cloud Translation API

```
curl -s -X POST \
-H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
-H "Content-Type: application/json; charset=utf-8" \
-d "{\"q\": [\"$task_5_sentence\"]}" \
"https://translation.googleapis.com/language/translate/v2/detect?key=${API_KEY}" \
-o "$task_5_file"
```

### Congratulations 🎉 for completing the Challenge Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/QuickGcpLab) & [Discussion group](https://t.me/QuickGcpLabChats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)
