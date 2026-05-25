# DYNAMO_DB
- It can take millions of requests per second
![alt text](dynamodb-images/image-51.png)
- auto scaling
-dynamo db is made of tables

## partition key
- decide server instance
## sort key
- it decides how data will be ordered with same partition key

## partition key+sort key-> primary key
![alt text](dynamodb-images/image-52.png)
- with the help of sort key .. we are able to create same category_name otherwise it was not possible 
![alt text](dynamodb-images/image-53.png)
![alt text](dynamodb-images/image-54.png)
- if u want to store metadata of blob like url, log ingestion

## capacity mode
### provisioned mode
- you yourself specify the number of reads and writes  that can happen on db instances
- you need to estimate the capacity yourself

### on demand
- reads and writes are automatically determined by aws
- pay as you go

### in provision capacity mode
- the read throughput

- the rcu(right capacity unit)-i
- the write throughput( write capacity unit)-insert,update,delte

- one wcu - one writes per second for upto 1kb of data
- then how much 20 records with atmost 2 kb -40wcu

- the default model in dynamodb- is strong constitency
- you can change to eventual consistency

-if one rcu is 1 strong consistenr read of atmost 4kb of data
## imp thing- rcu and wcu will get partitioned equally means u bought 1000 wcu and 10 partiotions then 100 wcu for

## question- what is the use of autoscaling in provisioned mode
- simple u will not get all the time maximum so u can turn on autoscaling
![alt text](dynamodb-images/image-55.png)

## dynamodb indexes
- lsi(local secondary index)-alternate sort key
- gsi(global secondary index)-alternate primary key- can be created after table

## to see data in dynamodb tbale
- there is left explore items go there

## you can write a sql query there also
partiQL editor

## DAX -Dynamo db Accelerator
-fully aws managed, in memory , highly available cache service for dynamodb
-microseconds latency for RW
- expiry time is 5 minutes
-![alt text](dynamodb-images/image-56.png)
- go to cluster and create a new cluster
-![alt text](dynamodb-images/image-57.png)
-high cost
-![alt text](dynamodb-images/image-58.png)

## TTL
- go to actions 
-![alt text](dynamodb-images/image-59.png)
- you have to enter epoch value 





