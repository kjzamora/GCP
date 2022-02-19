# GCP

## Table of Contents
- [Table of Contents](#table-of-contents)
  * [Setting gcloud CLI Environment and Variables](#setting-gcloud-cli-environment-and-variables)
    + [To define a variable named "MY_VARIABLE" within gcloud CLI:](#to-define-a-variable-named--my-variable--within-gcloud-cli-)
    + [To verify that variable was set:](#to-verify-that-variable-was-set-)
    + [To define the zone your instances will reside in:](#to-define-the-zone-your-instances-will-reside-in-)
    + [To define the region:](#to-define-the-region-)
  * [Creating a Single Instance](#creating-a-single-instance)
    + [The following command assumes you have a zone defined in the gcloud CLI:](#the-following-command-assumes-you-have-a-zone-defined-in-the-gcloud-cli-)
    + [If you would like to run a set of commands to say install something as soon as the instance is running you can add a startup script:](#if-you-would-like-to-run-a-set-of-commands-to-say-install-something-as-soon-as-the-instance-is-running-you-can-add-a-startup-script-)
  * [Buckets](#buckets)
    + [Creating a Bucket:](#creating-a-bucket-)
    + [Upload to a Bucket:](#upload-to-a-bucket-)
    + [Delete from a Bucket:](#delete-from-a-bucket-)
    + [Copy from one folder to another within a Bucket:](#copy-from-one-folder-to-another-within-a-bucket-)
    + [List Contents of the Bucket:](#list-contents-of-the-bucket-)
    + [Make an Object in your Bucket Public:](#make-an-object-in-your-bucket-public-)
    + [Remove Access from an Object in your Bucket:](#remove-access-from-an-object-in-your-bucket-)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

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
