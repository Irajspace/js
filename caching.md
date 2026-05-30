## Application level caching
```
const cache= new Map();
app.get('/users/:id',async(req,res)=>{
    const user_Id= req.params.id;


    if(cache.has(userId))
    {
        console.log("Cache hit")
        return res.json(cache.get(userId));
    }
    console.log('Cache Miss');

  const user = await db.query(
    'SELECT * FROM users WHERE id = ?',
    [userId]
  );

  cache.set(userId, user);

  res.json(user);
})


or pseudo code for redis
const cachedUser = await redis.get(`user:${userId}`);

if (cachedUser) {
  return res.json(JSON.parse(cachedUser));
}

const user = await db.query(
  'SELECT * FROM users WHERE id = $1',
  [userId]
);

await redis.set(
  `user:${userId}`,
  JSON.stringify(user),
  { EX: 60 } // 60 seconds TTL
);

```
## CACHING ORDER
```
Browser Cache
      ↓
CDN Cache
      ↓
Reverse Proxy Cache (Nginx)
      ↓
Application Cache (Redis)
      ↓
Database
```

```
Browser-cache
-immutable+ long max-age
1) here content of the url does not change
2)the browser can cache for almost 1 year

here lets say you want scrpit-v1.js so cache will see it has or not if it has it will not ask server 

- mutable cache no-cache
1) it is always server-validated
2)the contents of the url may change
3)so here cache asks server hey bro does the content of this page gets changed if so give me the new one and give the one to the user also .. if not so i will send mine 

-no store 
1) means not to cache at all
- egs banking system,html file

-must revalidate
1) means must validate after age expiry
2) otherwise its must re-valdate

-


```

## why the option (revalidate+max-age)
```
here this is wrong because when user asks for 3 pagees one is html,css,and another js file 
and u have changed 
max-age is relative to the response time, so if all the above resources are requested as part of the same navigation they'll be set to expire at roughly the same time, but there's still the small possibility of a race there. If you have some pages that don't include the JS, or include different CSS, your expiry dates can get out of sync. And worse, the browser drops things from the cache all the time
```

![alt text](image-21.png)
![alt text](image-22.png)

## diff between no-cache and no-store
![alt text](image-23.png)

## in the req header
-if cache set is public then it means it can be cached in between like proxies or cdn
-private - only in browser
-public- means reverse proxies or cdn can do it

## E-tags
-Revalidation mechanism
- they are generated to see if the same type hash value is coming from server. if so means same request with no change so we can give cache page
## Cache busting
- ususally next js files do like this so that cdn cant give stale data they hash the js files with random hashes
![alt text](image-24.png)

## CDN and reverse-proxies
-![alt text](image-25.png)
-![alt text](image-26.png)
=![alt text](image-27.png)
- ususally what happens we can do load balancing in network proxies itself then why do we load balancers before
-beacuse reveerse proxies works at application level
-and load balancer at aws works at network layer

## Database caching
-![alt text](image-43.png)



### why does caching is easier for bell-curve data rather than flat-line
```
The peak- (imaging the peak of bell curve. this data is regulary searched. since this is small. we can store small amount of data whereas for flat-line where each data has equal importance we have to advance strategies like lru )
for flat line 
If your traffic is flat or highly erratic, LRU won't help much. Advanced strategies might include:

Pre-fetching: Predicting what the user will do next and loading it into the cache before they ask for it (e.g., if they read page 1, proactively cache page 2).

Time-based or Event-based eviction: Heavily customizing exactly when and why data leaves the cache based on specific business logic rather than just basic popularity.

```
### Caching patterns-
```
Dynamic caching-
1)In a dynamic cache, the application treats the cache as the primary data store for both reading and writing.
2)ter the cache is updated, the cache itself (or a related process) is responsible for pushing that update down to the persistent data store (the main database).
Write-Heavy + Read-Immediately Workloads: For example, a multiplayer game leaderboard or a live sports score app. If a user updates their score and instantly refreshes the page, you want that new score waiting for them in the fast cache.

Static caching( catch-aside pattern)
1)As shown on the right side of the diagram, when an update occurs, the application bypasses the cache entirely and writes the new value directly to the persistent data store.
2)Because the data store now has the new value, the old value sitting in the cache is stale. Instead of updating the cache, the system simply deletes or invalidates the stale entry (represented by the large orange X over the cached item in the diagram).
Read-Heavy Applications: (e.g., User profiles, blog posts, product catalogs). Data is read 100 times for every 1 time it is updated.
```

### Caching stratgies