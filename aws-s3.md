## Amazon AWS S3 (simple storage service)
- if you want to store data in petabytes,gigabytes
- store blob(binary large object)
- a bucket contains collection of objects
-![alt text](image.png)

## why bucknet name should be diff for whole global space
- ![alt text](image-1.png)
- no conflict in dns resolution

## public access
-![alt text](image-2.png)

## when you upload that file
- you got public url to access that file

## how to access object from public url
-![alt text](image-3.png) 
- you have to add policy 
- means add policy generator
- in principal - type * means anu user
-![alt text](image-4.png)

## S3 versioning
- we can version our files on the bucket level and we have to manually enable it
- easly rollback
-![alt text](image-5.png)

## Replication strategies
-suppopse we have a bucket in region-1 
- we can replicate in diff bucket in same region or different region as abackup
- SRR- ( same region replication)
- CRR ( cross region replication)
- replication can be done in cross account also
- it is asynchronous process
- CRR- it can take more network bandwidth
- CRR- might be compliance issue
- lower latency issue
- SRR- prod data- test data backup
- log aggregation
- live replication
- by default only new objects added after replication is enabled after replication
-old objects can be replicated- (S3 batch replication)
-![alt text](image-6.png)
-![alt text](image-7.png)

### S3 storage classes
- we can created different type of s3 class based on access/storage pattern
