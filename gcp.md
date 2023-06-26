## Useful commands for GCP

gcp authorization:
```
gcloud auth login
```

check the current active project:
```
gcloud config get-value project
```

list all cloud projects:
```
gcloud projects list
```

switch to another cloud project:
```
gcloud config set project $PROJECT_NAME$
```

make a new bucket:
```
gsutil mb gs://bucket-name
```

list all the buckets:
```
gsutil ls
gcloud storage ls
```

get bucket size:
```
gsutil du -s gs://bucket-name
```

list all the objects in a bucket:
```
gsutil ls -r gs://bucket-name/**
```

remove a bucket:
```
gsutil rm -r gs://bucket-name
gsutil rb gs://bucket-name (remove only if the bucket is empty)
```

move all the data from one bucket to another:
```
gsutil cp -r gs://source-bucket gs://destination-bucket
```

remove a bucket:
```
gsutil rm -r gs://source-bucket (-r: recursive)
gsutil rm -a gs://source-bucket (-a: delete the objects and keep the bucket)
```

get lifecycle of a bucket:
```
gsutil lifecycle get gs://bucket-name
```

set lifecycle of a bucket:
```
cat /tmp/7day-lifecycle-configuration << EOF
{
  "lifecycle": {
    "rule": [{
      "action": {"type": "Delete"},
      "condition": {
        "age": 7
      }
    }]
  }
}
EOF
gsutil lifecycle set /tmp/7day-lifecycle-configuration gs://bucket-name
```

view bucket metadata:
```
gsutil ls -L -b gs://bucket-name
```

copy a file located on cloud to the current directory on your laptop:
```
gsutil cp /local/path bucket-name:cloud/path
```

send a file to the cloud:
```
gsutil cp bucket-name:cloud/path /local/path 
```



