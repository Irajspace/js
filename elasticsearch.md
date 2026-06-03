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
- a collection of documents called index
- When you search for information, you query data contained in an index.
- so let say you have infinte documents so good way is to partition the index into shards
- each shard is called lucene index on its own
- each node can have differnt shards of same index
-Splitting a 400 GB index into 1,000 shards, for example, would unnecessarily strain your cluster. A good rule of thumb is to limit shard size to 10–50 GB.
-![alt text](image-55.png)
![alt text](image-53.png)
![alt text](image-54.png)
- and each lucene index has segments where actual documents are stored
![alt text](image-51.png)
- here you see replication of one node is kept on a different node
-![alt text](image-52.png)

```
Cluster
│
├── Node 1
│   ├── Shard A
│   └── Shard B
│
├── Node 2
│   ├── Shard C
│   └── Shard D
│
└── Node 3
    └── Shard E

```

- Question
-is opensearch decides itself how to distribute the index on basis of shards and which shard will go to which node and how many nodes will be in one cluster

-Yes, OpenSearch automatically decides shard placement, but you decide how many nodes exist in the cluster.

Let's break it down.
-![alt text](image-56.png)
-![alt text](image-57.png)

## inverted index
-![alt text](image-58.png)


## BM25
-more occurence, more relevance
-penalises long documents
-how many times appeared in the document
-rarer words -more score
-![alt text](image-59.png)

## Creating index
-
```
let index="books"

var settings={

    settings:{
        index:{
            number_of_shards:4,
            number_of_repicas:2
        }
    }
}
var response= await client.indices.create({
    index=index.name,
    body=settings
})

```
## Indexing a document- means putting documents to the index(table)
```
var document = {
  title: "The Outsider",
  author: "Stephen King",
  year: "2018",
  genre: "Crime fiction",
};

var id = "1";

var response = await client.index({
  id: id,
  index: index_name,
  body: document,
  refresh: true,
});

Here refresh means as soon it is inserted it is ready for query as well
```

## Searching up a document

```
var query = {
  query: {
    match: {
      title: {
        query: "The Outsider",
      },
    },
  },
};

var response = await client.search({
  index: index_name,
  body: query,
});
The match query is a full-text search, not a strict, exact-string match. Here is a breakdown of how it works behind the scenes and how to actually get an exact match if you need one.

How the match Query Actually Works
When you index a document and when you search for it, the engine passes the text through an analyzer. By default, it does two main things:
Lowercases everything.
Splits the text into individual words (tokens).
So, your query "The Outsider" is broken down by the search engine into a list of words: ["the", "outsider"].
Because of this, a match query for "The Outsider" will successfully find documents with titles like:
"The Outsider" (Exact match)
"the outsider" (Case does not matter)
"Outsider" (It found one of the words)
"The Great Outsider" (It found both words, even with another word in the middle)

How to Get an Exact Match Instead
If you truly only want to match the exact phrase or the exact string, you have to use different types of queries:

1. match_phrase (Exact Words & Order)
If you want the words to appear in the exact order you typed them, you use a match_phrase query. This would match "The Outsider" or "Read The Outsider", but it would fail to match "The Great Outsider".
"match_phrase": {
  "title": "The Outsider"
}
2) term Query (100% Exact, Case-Sensitive Match)
If you want a strict, exact match where "The Outsider" only matches "The Outsider" (and fails on "the outsider" or "Read The Outsider"), you use a term query. This is usually run against a special sub-field called a keyword field, which skips the analyzer entirely.

"term": {
  "title.keyword": "The Outsider"
}

```




## updaing a document
```
we have seen while indexing we were writing body:document

means body:{title:""....}but here in updating why we are introducing doc inside body which is correct

When you use the index method, you are doing a Full Document Replacement (or creation). You are telling the database, "Take exactly what I am giving you and make this the new document."

Because the system expects the entire complete object, you just pass the raw document directly into the body:
// INDEXING (Full Replacement)
body: {
  title: "The Outsider",
  author: "Stephen King",
  year: "2018"
}

Updating (client.update) = "Here is a set of instructions."
When you use the update method, you are doing a Partial Update. You are telling the database, "Keep the existing document, but just change or add these specific pieces."

Because the Update API is very powerful, it can accept different types of update instructions. Wrapping your fields inside "doc": {} explicitly tells the engine: "I am providing a partial document. Please merge these fields into the existing one."
// UPDATING (Partial Merge)
body: {
  doc: { 
    year: "2019" // Only updates the year, leaves title and author alone
  }
}
Why does it need to know it's a "doc"?
Because you don't have to use doc. The Update API also allows you to update documents using scripts (code that runs on the server to calculate a new value).

If you wanted to increase a book's "view count" by 1, instead of using doc, you would pass a script:
body: {
  script: {
    source: "ctx._source.views += 1"
  }
}

```

## Deleting a document
```
var response = await client.delete({
  index: index_name,
  id: id,
});

```
## Deleting an index
```
var response = await client.indices.delete({
  index: index_name,
});


```