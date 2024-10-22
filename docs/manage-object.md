# Manage objects

Managed objects in the Google Distributed Cloud (GDC) air-gapped storage buckets.

## Table of Content
- [Prerequisite](#prerequisite)
- [IAM](#iam)
- [Upload objects to storage buckets](#upload-objects-to-storage-buckets)
- [Download objects from storage buckets](#download-objects-from-storage-buckets)
- [List objects in storage buckets](#list-objects-in-storage-buckets)
- [Copy, modify, and move objects](#copy-modify-and-move-objects)
- [Known Issue](#known-issue)

## Prerequisite
- A valid [bucket](/docs/object-storage.md) 
- Unique bucket name within the project

## IAM
- **Project Bucket Object Viewer**: This lets a user list all buckets in the project, list objects in those buckets, and read objects and object metadata. It does not let you write operations on objects. For example: uploading, overwriting, deleting.
- **Project Bucket Object Admin**: This lets a user list all buckets in the project, and write and read operations on objects. For example: uploading, overwriting, deleting.

## Upload objects to storage buckets
1. In the navigation menu, click Object Storage.
2. Click the name of the bucket you want to upload the object to.
3. Optional: If you want to create a folder to store your object, click Create folder > enter a folder name > click Create.
4. Click Upload file directly, or navigate into the folder you just created and then click Upload file.
5. Select the desired file and click Open.
6. Wait for the confirmation message that the upload was successful.

## Download objects from storage buckets
1. In the navigation menu, click Object Storage.
2. Click the name of the bucket containing the objects.
3. Select the checkbox next to the name of the object to download.
4. Click Download.

## List objects in storage buckets
1. In the navigation menu, click Object Storage.
2. Click the name of the bucket containing the objects.
3. Wait to be redirected to the Bucket details page with objects listed in a table.
4. Click on an object's name and select either the Live Object tab or Version history tab to view further details.

## Copy, modify, and move objects
Copy an object:

```bash
gdcloud storage cp FILE  [FILE...] s3://BUCKET [/PREFIX ]
```

Modify an object's metadata:
```bash
gdcloud storage objects update s3://BUCKET1/OBJECT --custom-metadata=Key1=Value1
```

Move an object:
```bash
gdcloud storage mv s3://BUCKET1/OBJECT1 s3://BUCKET2[/OBJECT2]
```
---
[Top](#) | [Home](/README.md) | [Object Storage](/docs/object-storage.md) 

[Source](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/upload-download-storage-objects) | [Source](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/list-storage-objects) | [Source](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/copy-mod-storage-objects)
