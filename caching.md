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