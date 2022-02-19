# GCP


</br>

## Setting gcloud CLI Environment and Variables

### To define a variable named "MY_VARIABLE" within gcloud CLI:
```go
export MY_VARIABLE=<your_VARIABLE>
```
### To verify that variable was set:
```go
echo $MY_VARIABLE
```

### To define the zone your instances will reside in:
```go
gcloud config set compute/zone $ZONE
```

### To define the region:
```go
gcloud config set compute/region $REGION
```


</br>

## Creating a Single Instance
### The following command assumes you have a zone defined in the gcloud CLI:

```go
gcloud compute instances create $INSTANCE_NAME --machine-type $MACHINE_TYPE --image-family $IMAGE
```
### If you would like to run a set of commands to say install something as soon as the instance is running you can add a startup script:
```go
gcloud compute instances create $INSTANCE_NAME --machine-type $MACHINE_TYPE --image-family $IMAGE --metadata-from-file startup-script=startup.sh
```


</br>

## Buckets
### Creating a Bucket:
A bucket must have a globally unique name. A simple way is to define the bucket name is basing it off your Project ID which must also be globally unqiue:
```go
export BUCKET=<project_id-bucket_name>
gsutil mb -p $PROJECT gs://$BUCKET
```
### Upload to a Bucket:
From the cloud shell:
```go
gsutil cp $FILENAME gs://$BUCKET
```

### Delete from a Bucket:
From the cloud shell:
```go
gsutil rm gs://$BUCKET/$FILENAME
```

### Copy from one folder to another within a Bucket:
From the cloud shell:
```go
gsutil cp gs://$BUCKET/$FILENAME gs://$BUCKET/$FOLDER_NAME/
```

### List Contents of the Bucket:
From the cloud shell:
```go
gsutil ls gs://$BUCKET
```

### Make an Object in your Bucket Public:
From the cloud shell:
```go
gsutil acl ch -u AllUsers:R gs://$BUCKET/$FILENAME
```

### Remove Access from an Object in your Bucket:
From the cloud shell:
```go
gsutil acl ch -d AllUsers gs://$BUCKET/$FILENAME
```
