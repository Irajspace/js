# what is wrong in other db
- unka through put is very less, means jyadatar messages tm ni bhej skte
- sb ke liye kafka use kyon ni use krte kafka -
-beacuse it can hold temporray storge and also queuing is slow
-

# topics
- topics store data in logs
-![alt text](image-12.png)
-immutable
-you can also derive topics from other topics
-![alt text](image-13.png)
- logs are not like queue means once data is read it is still there
-![alt text](image-14.png)
-logs can be deleted after certain period
-default is 7 days
-![alt text](image-15.png)

## partitions
-location wise kr skte ho
- name wise kr skte ho
- parttion takes that single log and breaks into multiple partition
-support 2 million partition
-if message has not key then it will be distributed in round robin across all partition
- 1 partition ek hi consumer group ko ja skta hai

## consumer group
![alt text](image-19.png)
- self balancing ek group ke liye hoti hai
- pub/sub mein ek producer hota hai and multiple consumers hote hain

## brokers
-![alt text](image-16.png)
-![alt text](image-17.png)
- they form kafka clusters
- these are nothing but the things that get message from producer and sent it to consumer

## replication
-![alt text](image-18.png)
- the darker one is read replica

## producers



