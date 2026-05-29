# How to tackle interview
## ![alt text](image-20.png)
~~~
Requirements-> Core entities ->(API or interface)->Data flow->High Level Design->Deep dives
~~~

## Requirements
### Functional requirements

```
1) Here you have to ask the core features of the product
2) Does user should be able to post tweets
3) Does user be able to see tweets from users they follow

For cache
1)Clients should be able to insert items
2)Clients should be able to set expirations
3)Clienst should be able to read items

```
### Non-functional requirements

```
1) The system should be highly available , prioritizing availability over consistency
2)the system should be able to support 100 M+ DAU
3)low latency



```
### there are many ways u can find how to find nfr
```
 - The worst case scenario method
 - What is the absolute worst thing that could happen to a user using this system?
 - if the worst thing is losing money- consistency or durability is happening
 - if the worst thing is staring at a loading screen for 5 seconds- latency is top priority


```
### CAP theorem(Consistency vs Avaialabilty)
- When a network partition happens(egs- server loose connection  to each other). do you keep consitency or availanbiity
-Consistency-> financial system,booking a flight seat
-availaiabilty- streaming services

### Scalabiluty-
- for read heavy- 100 reads for every 1 write->(twitter, youtube)-> YOu will need heavy caching and CDN
-