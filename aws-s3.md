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
- when u are uploading something , there are some properties option
- ![alt text](image-8.png)
- S3 standard(general)-99..99% availabilty - is used for frequent access, low latency,high throughput
- S3 standard(infrequent access)-good for data which is not frequently access but requires rapid access when needed, availiabilty-99.99%,low cost 
- S3 one zone infrequent access
- S3 glacier instant retreival-low cost , ms retrieval,very less access
- S3 glacier flexible retreival-(1-5)best, 12hr bad,very less access
- S3 glacier deep archive- 48 hr retreival ,very less access
- S3 intelligent tiering- automatically aws will determine which will be fast, but will cost due to aws management

- they are identfied by (durability and availability)
- for durability for all storage classes it is 99.99%
-for availability it is different for storage classes - means how much it is readily available 

### life cycle route
- in management
-![alt text](image-9.png)
-![alt text](image-10.png)
-![alt text](image-11.png)
- so what it does let say you can urself determine after how many days you want to transitition in which storage class
-1) transpiration access- storage classes gets changed
-2) expiration access - older versions gets deleted

### S3 update notifications
-this can work as a trigger( producer)
- assume we do some actions on objects store in a bucket. and we want to fire notifications, this can be achiedved thrugh event listeners
- on diff services - (SNS,SQS,lambda)consumption

### AWS S3 performance
-S3 auto scales for reducing latency
- for any read/get request-5500 req per second per prefix
-write-3500 req per second
- system->s3 ( u can upload in multiparts)
- normal flow kya hai( client->backend->s3)
-client->backend se presigned url aur backend->s3->backend->client ...phir client diretcly frontend se upload kr skta hai
- S3 byte range fetch

