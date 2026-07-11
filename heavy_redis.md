# What is cache-aside pattern?
``
    The cache-aside pattern is lazy-loading caching strategy where the application is responsible for reading and writing to both cache and database

    The goal of this design pattern is to set -up optimal caching(load as-you-go) for better read operations. the cache is populated when data is requested and not found in redis .. then application fetches it from the database and store it in redis.

``
![alt text](heavy-redis-images/image-31.png)
![alt text](heavy-redis-images/image-32.png)

# SESSION_MANAGEMENT

![alt text](heavy-redis-images/image-33.png)

# SORTED_SETS
![alt text](heavy-redis-images/image-34.png)

# DATA_PERSISTENCE
![alt text](heavy-redis-images/image-35.png)

``An AOF(Append-only File) maintains a record of write operations. This allows the data to be restored by using the record the reconstruct the database up to the point of failure``

![alt text](heavy-redis-images/image-36.png)
![alt text](heavy-redis-images/image-37.png)
![alt text](heavy-redis-images/image-38.png)
👉 RDB is periodic by design (snapshot-based)
👉 AOF is continuous logging with optional periodic disk syncing
![alt text](heavy-redis-images/image-39.png)
![alt text](heavy-redis-images/image-40.png)

