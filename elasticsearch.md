# elastic search
- built on top of apache lucene
- apache 2 license

- Node -> a single running instance of elasticsearch file
- Cluster -> a collection of one or more nodes working under the same cluster.name

![alt text](image-49.png)

```
curl -XGET 'http://localhost:9200/_count?pretty' -d '
{
    "query": {
        "match_all": {}
    }
}'
### 2. Understanding the Elasticsearch Response
* Elasticsearch responds with a standard HTTP status code (such as `200 OK`) along with a JSON-encoded response body (unless a `HEAD` request was sent).
* The example response block shows:
  * `"count" : 0` – No documents have been matched yet.
  * `"_shards"` metadata – Indicating that 5 total shards were checked, all 5 were successful, and 0 failed.

---

### 3. Viewing HTTP Headers
The text notes that standard terminal `curl` commands hide HTTP headers by default. If a developer needs to view headers, they should include the `-i` (include) switch in their command:
```bash
curl -i -XGET 'localhost:9200/'

```

## stores in JSON
```
{
    "email":      "john@smith.com",
    "first_name": "John",
    "last_name":  "Smith",
    "info": {
        "bio":       "Eco-warrior and defender of the weak",
        "age":       25,
        "interests": [ "dolphins", "whales" ]
    },
    "join_date": "2014/05/01"
}

```

## example
```
Relational DB       Elasticsearch/OpenSearch

Database      ->    Index
Row           ->    Document
Column        ->    Field
An Elasticsearch cluster contains multiple indices (databases), which contain multiple types (tables), which hold multiple documents (rows), which are made up of multiple fields (columns).


```
![alt text](image-50.png)



### Starting opensearch
