# Object Storage

Grant and obtain access for Google Distributed Cloud (GDC) air-gapped storage buckets.

## Table of Content
- [Prerequisite](#prerequisite)
- [IAM](#iam)
- [Create a bucket](#create-a-bucket)
- [Create a WORM bucket](#create-a-worm-bucket)
- [List storage buckets](#list-storage-buckets)
- [View bucket configurations](#view-bucket-configurations)
- [Delete a bucket](#delete-storage-bucket)
- [Manage objects](/docs/manage-object.md)
- [Known Issue](#known-issue)

## Prerequisite
- Valid project with IAM permissions
- Unique bucket name within the project

## IAM
- **Project Bucket Admin**: This lets users manage all buckets in the given namespace, as well as all the objects in those buckets.

## Create a bucket
1. In the navigation menu, click Object Storage.
2. Click Create Bucket.
3. In the bucket creation flow, assign a name unique across all buckets within the project.
4. Enter a description.
5. Optional: Click the toggle to set a retention policy and enter your preferred number of days. Contact your IO if you need to exceed retention policy limits.
6. Click Create. A success message appears and you are directed back to the Buckets page.

To verify that you have successfully created a new bucket, refresh the Buckets page after a few minutes and check that the bucket state updates from Not ready to Ready.

## Create a WORM bucket
A WORM bucket ensures that nothing else overwrites objects and it retains them for a minimum period of time. Audit logging is an example use case for a WORM bucket.

1. Set a retention period when creating the bucket. For example, the following example bucket has a retention period of 365 days.

```yaml
apiVersion: object.gdc.goog/v1
kind: Bucket
metadata:
  name: foo logging-bucket
  namespace: foo-service
spec:
  description: "Audit logs for foo"
  storageClass: Standard
  bucketPolicy :
    lockingPolicy :
      defaultObjectRetentionDays: 365
```
2. Grant the project-bucket-object-viewer role to all users who need read-only access:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  namespace: foo-service
  name: object-readonly-access
roleRef:
  kind: Role
  name: project-bucket-object-viewer
  apiGroup: rbac.authorization.k8s.io
subjects:
- kind: ServiceAccount
  namespace: foo-service
  name: foo-log-processor
- kind: User
  name: bob@example.com
  apiGroup: rbac.authorization.k8s.io
```

3. Grant the project-bucket-object-admin role to users who need to write content to the bucket:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  namespace: foo-service
  name: object-write-access
roleRef:
  kind: Role
  name: project-bucket-object-viewer
  apiGroup: rbac.authorization.k8s.io
subjects:
- kind: ServiceAccount
  namespace: foo-service
  name: foo-service-account
```

## List storage buckets
1. In the navigation menu, click Object Storage. All buckets you have access to are listed in a table.

## View bucket configurations
1. In the navigation menu, click Object Storage.
2. Click the name of the bucket of which you want to view the details.
3. Wait to be redirected to a detailed view page.

## Delete storage bucket
1. In the navigation menu, click Object Storage.
2. Click Delete at the end of the row of the bucket to be deleted.
3. t a few minutes and refresh the page to check that the bucket is deleted.

## Known Issue
- You can only specify the Encrpytion v1 or v2 using CLI

---
[Top](#) | [Home](/README.md) | [Manage object](/docs/manage-object.md)

[Source](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/create-storage-buckets) | [Source](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/list-view-storage-buckets) | [Source](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/delete-storage-buckets)
