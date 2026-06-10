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
2)the system should be able to support 100 M+ DAU(daily active users)
3)low latency



```
### there are many ways u can find how to find nfr(non-functional requirement)
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

### fault torenace
-7. Fault Tolerance

What it is: The system's ability to continue operating properly in the event of hardware or software failures.

### Capacity estimation

-dont do math in early processing ( back of envelope calculation)

```
Many traditional interview guides tell you to immediately calculate Storage, Daily Active Users (DAU), and Queries Per Second (QPS) right after gathering requirements.

The authors argue this is often a trap. If you spend five minutes calculating that your system has 100,000 QPS and requires 5 Petabytes of storage, just to conclude, "Okay, this is a large system," you have wasted valuable time. The interviewer already knew it was a large distributed system, and you've only proven that you can multiply numbers.
I'm going to hold off on upfront capacity estimations to save time, but I will do the math later when we hit a specific design bottleneck."

```

### Core entities
```
Core entities are the foundational "building blocks" or the primary data objects your system will handle. They are the things your system will eventually save in a database (Data Model) and send back and forth over the network (APIs).

How to find them: The text offers a great trick—look at your functional requirements and pick out the actors (who is using the system) and the nouns (what resources they are interacting with).

Example: If your functional requirement is "Users can post a tweet and follow other users," your core entities are naturally going to be User, Tweet, and Follow.

Dont overengineer
Many candidates make the mistake of spending 10 minutes writing out every single database column (e.g., user_id, first_name, last_name, created_at, profile_picture_url).

The text advises against this because "you don't know what you don't know." As you move into drawing the High-Level Design later in the interview, you will inevitably realize you need new tables or fields to make things work.

The Strategy: Treat this as a simple, bulleted rough draft. Just jot down the names of the main entities to get on the same page as your interviewer, and tell them you will flesh out the specific columns later when the architecture is clearer.




```
# When do we use RPC(REMOTE PROCEDURE CALLS)

```
Functions
1) Unary GRPC-(single request and response)
2) Server streaming-the client sends a single request. The server responds with a stream of messages. The client reads from the returned stream until there are no more messages.
The video streaming example from your presentation image is perfect here. You click "Play" on a YouTube video (one request), and Google's servers continuously send you chunks of video data (a stream of responses) so you can watch it without downloading the entire 2GB file first.
3) Client streaming-
he client writes a sequence of messages and sends them to the server using a provided stream. Once the client has finished writing the messages, it waits for the server to read them all and return its single response.
Uploading a massive high-resolution image to a server, or an IoT temperature sensor constantly streaming its readings to a central server which replies with an "Acknowledged" status once a minute.
4) Bidirectional-
Both the client and the server send a sequence of messages using a read-write stream. The two streams operate completely independently, meaning the client and server can read and write in whatever order they like.
A multiplayer video game where the client is constantly streaming player movements to the server, and the server is simultaneously streaming the movements of all other players back to the client


Here in all rest of protocols
-1) they need client librarires which are hard to maintain and patch libraries
-2) they are not comptabile all languages
-3) for rest api they need http library
-4)these all requests are handled by browser client .. they take requst . they se http requst they verify tls certiifcates
but lets say it is python client , go client

why grpc?
-one library for popular languages
-How gRPC Solves This Automatically
If this company used gRPC instead of REST, this drift would be impossible. The backend team would update the .proto file:

Protocol Buffers
message User {
  int32 user_id = 1; // Changed to int
  string name = 2;
  int32 user_age = 3; // Added age
}
The moment they save this file, the gRPC compiler automatically generates the updated Java code and the updated Python code simultaneously. Both teams get the exact same update at the exact same time with zero manual coding, eliminating the nightmare entirely.

Have you ever had to deal with an API suddenly changing its response structure while you were building something?

main advantage
That is the absolute core superpower of gRPC. The .proto file acts as the single source of truth for your entire system.

Here is the exact workflow of how it happens:

You make a change: You edit the .proto file (for example, adding string email = 4;).

You run the compiler: You run a single terminal command using the gRPC compiler tool (called protoc).

Code is generated: The compiler instantly generates the updated, ready-to-use code (the schemas, classes, methods, and network routing logic) for Python, Java, Go, Node.js, or whatever languages your team uses.
```


```
here in image u see authentication service needs to talk to notification service
every languaage has its own HTTP library and request and every one has to talk to notification to talk to client make massive no of request
```

![alt text](image-61.png)
![alt text](image-62.png)

## Problem with JSON
![alt text](image-63.png)
-grpc(http/2)
```
serialization deserialisation (grpc framework)uses protobuff
protobuf
keys ko integer mein convert krta hai


```
![alt text](image-64.png)


### GraphQL
```
let say tmhe server se kuch chaiye like todo
toh woh pura bhej dega
1) userid,title,completed,id
but tmhe sirf title chaiye matlab fetch hi kyun kiya

```

# why you need to take userid and name from backend ..adds authentiation... and not directly take from frontend
```
const jwt = require("jsonwebtoken");

function authenticate(req, res, next) {
    const authHeader = req.headers.authorization;

    const token = authHeader.split(" ")[1];

    try {
        const decoded = jwt.verify(token, SECRET_KEY);

        req.user = decoded;   // { userId: "alice" }

        next();
    } catch (err) {
        return res.status(401).send("Invalid token");
    }
}
app.delete(
    "/posts/:postId",
    authenticate,
    async (req, res) => {

        const postId = req.params.postId;

        const userId = req.user.userId;

        const post = await Post.findById(postId);

        if (!post) {
            return res.status(404).send("Post not found");
        }

        if (post.owner !== userId) {
            return res.status(403).send("Forbidden");
        }

        await Post.deleteOne({ id: postId });

        res.send("Deleted");
    }
);

here u ques might be what is stored in decoded?
{
  userId: 'alice',
  role: 'admin',
  iat: 1750000000
}

```
Data flows
```
How to do it: Don't draw it yet. Just write a simple numbered list, like the web crawler example in the image.

Fetch seed URLs.

Download HTML.

Extract new links from HTML.

Save data to a database.

Put the newly extracted links back into a queue to repeat the process.

By listing these steps out loud, you are essentially creating a checklist for the High-Level Design drawing phase. You now know you will need a component to fetch URLs, a worker to parse HTML, and a queue to manage the new links.


```
![alt text](image-65.png)


## networking essentials
```
1. Layer 3: Network Layer (The Post Office)

What it is: This layer is primarily about IP (Internet Protocol). It handles routing and addressing. Think of it as the postal service figuring out how to get a package from New York to Tokyo by hopping through different mail sorting facilities (routers).

Interview Relevance: You don't usually spend much time here in an interview, but you must implicitly understand that every component you draw (servers, databases) needs an IP address to find each other. The text mentions InfiniBand for ML—this is a great buzzword to know if you are interviewing for heavy AI/Machine Learning infrastructure roles, as it's much faster than standard IP networking.

2. Layer 4: Transport Layer (The Delivery Method)

What it is: Once Layer 3 finds the destination, Layer 4 decides how to deliver the data.

Interview Relevance (Crucial): You will frequently be asked to choose between the main protocols here:

TCP (Transmission Control Protocol): Reliable, ordered, and checks for errors. If a packet of data is lost, TCP resends it. Most of the web (including HTTP) runs on TCP.

UDP (User Datagram Protocol): Fast but unreliable. It just fires data at the destination and doesn't care if it actually arrives or in what order.

3. Layer 7: Application Layer (The Language)

What it is: This is the layer you interact with as a software engineer. It builds on top of TCP or UDP to provide meaningful abstractions.





```
## How a simple request gets the response

```
-first dns convert the domain name into ip address  called dnsresolution
-then client initiates a 3-way handshake with the server 
-TCP Handshake: The client initiates a TCP connection with the server using a three-way handshake:
SYN: The client sends a SYN (synchronize) packet to the server to request a connection.
SYN-ACK: The server responds with a SYN-ACK (synchronize-acknowledge) packet to acknowledge the request.
ACK: The client sends an ACK (acknowledge) packet to establish the connection.

HTTP Request: Once the TCP connection is established, the client sends an HTTP GET request to the server to request the web page.
Server Processing: The server processes the request, retrieves the requested web page, and prepares an HTTP response. (This is usually the only latency most SWE's think about and control!)
HTTP Response: The server sends the HTTP response back to the client, which includes the requested web page content.

HTTP Request: Once the TCP connection is established, the client sends an HTTP GET request to the server to request the web page.
Server Processing: The server processes the request, retrieves the requested web page, and prepares an HTTP response. (This is usually the only latency most SWE's think about and control!)
HTTP Response: The server sends the HTTP response back to the client, which includes the requested web page content.


Connections are Expensive: A connection between a client and a server isn't just a tube; it's a state that consumes memory and resources on both ends.

The Reconnection Penalty: If you close a connection after every single API request, you have to pay the "TCP Handshake" latency tax all over again for the next request.

The Solution: The text mentions HTTP keep-alive and HTTP/2 multiplexing. These are techniques to hold a connection open so multiple requests can flow through it without repeating the setup phase. If you are designing a chat app or a live stock ticker, you will rely heavily on persistent connections (like WebSockets) to avoid this massive overhead.

```

## HTTP 2 multiplexing
```
The Problem: HTTP/1.1 and the "Single Lane"
Imagine you are loading a modern webpage like Amazon.com. Your browser doesn't just make one request; it might need 50 different things (the HTML, the CSS file, a Javascript file, and 47 different product images).

In the old days of HTTP/1.1, a single TCP connection could only handle one request at a time.

Your browser says: "Give me the HTML."

It has to sit and wait for the entire HTML file to download before it can say "Okay, now give me the CSS file."

This is called Head-of-Line Blocking. If one large image gets stuck in traffic, everything else behind it has to wait.

The Problem: HTTP/1.1 and the "Single Lane"
Imagine you are loading a modern webpage like Amazon.com. Your browser doesn't just make one request; it might need 50 different things (the HTML, the CSS file, a Javascript file, and 47 different product images).

In the old days of HTTP/1.1, a single TCP connection could only handle one request at a time.

Your browser says: "Give me the HTML."

It has to sit and wait for the entire HTML file to download before it can say "Okay, now give me the CSS file."

This is called Head-of-Line Blocking. If one large image gets stuck in traffic, everything else behind it has to wait.


```

## DHCP( Dynamic Host Configuration Protocol)
```
THe servers get their IP addresses from a DHCP server when they boot up
Think of a DHCP server as a receptionist at a hotel handing out room keys. When a computer connects to a network, it asks the DHCP server, "Who am I?" and the server hands it an IP address to use while it's connected

Private vs. Public IP Addresses
This is the most critical takeaway from the text for your interviews.

Private IPs: You can set up a cluster of 100 database servers in a warehouse and give them whatever IP addresses you want (e.g., 10.0.0.1, 10.0.0.2). However, these are internal to your network. If a user in London tries to access 10.0.0.1, the global internet has no idea where that is.

Public IPs: If you want your servers to be accessible from the open internet, they need a Public IP. These must be globally unique and are distributed by authorities called RIRs (Regional Internet Registries)

The internet's core routers maintain massive maps (using a protocol called BGP, though you don't need to memorize that for basic HLD).

Because Apple owns the entire block of IP addresses starting with 17 (e.g., 17.x.x.x), every major router in the world has a simple rule: "If a packet's destination starts with 17, pass it toward Apple's network." ---

```

## transport layer
```
When data is sent over the internet, it gets chopped up into tiny pieces called packets. These packets don't always take the same physical route across the globe, meaning Packet #5 might arrive before Packet #2.

TCP- here if any packet doesnt arrived at the end .. it pauses and asks for again
how does the ordering
-The Receive Buffer (The Waiting Room)
When the packets arrive at the server, they don't immediately go straight into the application (like a web browser or a game). Instead, TCP catches them and puts them into a staging area in the server's memory called the Receive Buffer.

Here is how the server handles the chaos:
The "Next Expected" Rule: The server knows it is waiting for Sequence #1.
Out of Order Arrival: Let's say Sequence #3 and #4 arrive first because they took a faster route across the internet. The server does not throw them away, but it also doesn't let the application see them yet. It puts them in slots #3 and #4 in the waiting room.
Filling the Gap: The server pauses and waits. Once Sequence #1 and #2 finally arrive, it drops them into slots #1 and #2.
Delivery: Now that the sequence is complete (1, 2, 3, 4), TCP scoops them all up, stitches them together in perfect order, and hands the complete, correct data to the application.

Stateful Connection: Unlike UDP's "spray and pray," TCP maintains a strict "state." Both the client and the server keep track of exactly what has been sent, what has been received, and what is missing.
Flow Control (Protecting the Receiver): Imagine a supercomputer trying to send a massive file to an old, slow smartphone. If the supercomputer blasts data too fast, the phone's memory will overflow and crash. TCP uses Flow Control to let the phone say, "Whoa, slow down, my receive buffer is almost full!" The sender will dynamically slow its transmission rate to match what the receiver can handle.
Congestion Control (Protecting the Network): Imagine millions of people trying to stream Netflix at 8:00 PM. The routers and cables in the middle of the internet get jammed. If TCP detects that packets are dropping because the network itself is congested, it will throttle back the speed for everyone slightly to prevent the entire internet backbone from collapsing.



QUIC- HTTP/3 connection built on UDP with reliability of TCP


UDP-
isse chlega fortnite, doesnt care if packet arrives or not
4 characterisitics-
a) connectionless- no tcp handshake save time
b)no gurantee of delivery
c)no ordering
d)fastest way

where to use- VOIP or zoom call, if there is sound glitch doesnt matter,gaming

The Limitation: Standard web browsers (Chrome, Safari) generally do not let developers open raw UDP connections. (The only major exception is WebRTC, a specific protocol used for browser-to-browser video chats)
The Interview Solution: If an interviewer asks you to design a live reaction system for both mobile apps and a website, you should propose a hybrid approach. Tell them: "I will use fast UDP for the iOS/Android apps, but for the web browser users, I will fall back to a TCP-based connection (like WebSockets) and batch the reactions together every few milliseconds to save bandwidth." ### 2. The TCP Workhorse (State & Ordering)
Since we just covered how TCP orders packets with Sequence Numbers and a Receive Buffer, this section should sound very familiar!

What is Telemetry? Imagine you are designing a system to monitor the health of 100,000 servers. Every server sends its CPU temperature to your database every single second.

the hybrid
When the user opens the app, logs in, loads their contacts, and sends a chat message, that data must be perfectly reliable. You route this traffic over standard TCP.
The moment they click "Join Video," the actual webcam and microphone streams are blasted over UDP (or WebRTC) because speed becomes the only thing that matters.


```

## Load balancers
```
Layer 4 Load Balancers: These operate primarily in or near Kernel Space. They only look at the IP address and the port (e.g., "Send this TCP packet to Server B"). Because they don't drag the data up into User Space to read it, they are astonishingly fast and can handle massive amounts of traffic with very little CPU power.

Layer 7 Load Balancers: These operate in User Space. They fully open the HTTP request and read the contents (e.g., "Oh, the user is requesting the /images URL, let me route this to the Image Server"). Because they process this in User Space, they are much "smarter," but they are slower and require more CPU power to run.

```
## THe HTTP protocol
```
The most critical sentence in this image is: "HTTP is a stateless protocol." Wait, didn't we just learn that TCP (the layer underneath HTTP) creates a stateful connection? Yes! This is a classic interview concept:

Layer 4 (TCP) is Stateful: The pipe itself remembers that it is open and tracks the sequence of packets.

Layer 7 (HTTP) is Stateless: The messages sent through that pipe have no memory of each other. If you ask the server for your profile picture, and then one millisecond later ask for your friend's profile picture, the HTTP server treats those as two completely independent events. It doesn't say, "Oh, it's the same guy from a millisecond ago."


```

## Request modes
```
GET: Request data from the server. GET requests should be idempotent and don't have a body.- idempotent means at last final result is same u will get same user
POST: Send data to the server.- non-idempotent .. final result will not be same
PUT: Update data on the server.- idempotent .. final result will be same if we do multiple times
PATCH: Update a resource partially.
DELETE: Delete data from the server. DELETE requests should be idempotent.- here user 1 deleted once if u send multiple user 1 will not be there

```

## status codes
```
Success (2xx)
200 OK: The request was successful
201 Created: The request was successful and a new resource was created
Moved (3xx)
302 Found: The requested resource has been moved temporarily
301 Moved Permanently: The requested resource has been moved permanently
Client Error (4xx)
404 Not Found: The requested resource was not found
401 Unauthorized: The request requires authentication
403 Forbidden: The server understood the request but refuses to authorize it
429 Too Many Requests: The client has sent too many requests in a given amount of time
Server Error (5xx)
500 Server Error: The server encountered an error
502 Bad Gateway: The server received an invalid response from the upstream server


```
### Content negotiation
```
The best example of this is Content Negotiation.

The Problem: Sending massive amounts of JSON data over the internet is slow. It would be much faster if the server could compress the data into a ZIP file before sending it. But what if an older client app doesn't know how to unzip it?

The Solution: The client sends an Accept-Encoding: gzip header. This politely tells the server, "Hey, if you know how to compress things using gzip, I know how to read them." The server zips the data, attaches a Content-Encoding: gzip header to the response, and sends it.

Interview Context: This demonstrates Graceful Degradation. If an old mobile phone connects and doesn't send that header, the server safely falls back to sending plain, uncompressed text. Your API didn't crash; it just adapted.

```

### The red box
```
This is the most critical part of the image, and it loops back to the exact vulnerability we discussed earlier: IDOR (Insecure Direct Object Reference).

It is very easy to confuse encryption with trust.

What HTTPS does: It guarantees that nobody between the user and your server can read or alter the data.

What HTTPS does NOT do: It does not guarantee that the person sending the data isn't a hacker.

The Scenario: A hacker logs into their own account. Because they are logged in, they have a valid, encrypted HTTPS connection to your server. They then intercept their own request before it leaves their computer and change the JSON body from {"delete_user": "hacker123"} to {"delete_user": "alice"}. HTTPS will happily encrypt that malicious payload and safely deliver it to your server.

The Lesson: Never trust the request body for sensitive actions. Always figure out who the user is by verifying their secure Authentication Token (which they cannot forge) on the backend.


```
### REST APP
```
Good: /users or /tweets

Bad: /createNewUser or /getTweets
GET /users/{id}.

Creating (POST /users):here server generates the ID and save it

in names remember dont use verbs 
how to name to start game?
Verb: PATCH

URL: /games/123

JSON Body: ```json
{
"status": "ACTIVE"
}


```


### Graphql-solution
```
In a perfect REST API, every specific resource has its own unique URL (e.g., /profile, /status, /groups).
in graphql u can only do post which can be mutated into insert,delte
Look at the "App View" in the drawing. Imagine you are opening the Facebook app to look at a friend's profile. That single screen needs their profile picture, their current status, and a list of the 3 groups they are in.

The REST Way: Because REST forces you to hit specific endpoints for specific data, your mobile app has to make 5 separate trips to the server:

Fetch the profile (/profile/{id})
Fetch the status (/status/{id})
Fetch group 1 (/group/{id1})
Fetch group 2 (/group/{id2})
Fetch group 3 (/group/{id3})

Think back to what we just learned about Layer 4 Networking and Latency. Every single one of those arrows in the diagram represents a network request that has to travel across the internet, get processed, and travel back.
If each round-trip takes 100 milliseconds, forcing the client to make 5 sequential trips means the user is staring at a blank loading screen for half a second. This is brutal for mobile users on slow 3G networks.

The Solution: GraphQL

- heavytyped( schema based design )
- transport agnostic( can be based on HTTP, raw tcp, websockets,udp)

Underfetching-
GraphQL flips the entire REST paradigm upside down. Instead of having dozens of rigid endpoints (/users, /posts, /groups), a GraphQL server usually only has one single endpoint (e.g., POST /graphql).

Instead of the server dictating what data you get, the client dictates exactly what it wants.

The GraphQL Way: The mobile app sends one single request to the server that essentially says: "Give me user 123's profile, their status, and the names of all their groups."

The server does all the heavy lifting of gathering that diverse data internally, packages it into one neat JSON payload, and sends it back in a single round-trip.

the trade-offs
Because GraphQL is significantly harder to build and cache on the backend. With REST, you can easily cache a popular response (like GET /tweets/1) in a CDN so it never even hits your server. Because GraphQL queries are totally custom and bundled together, caching them at the network layer is incredibly difficult.

Overfetching-
The REST Scenario: Imagine you are building a mobile app screen that shows a list of users, but you only need to display their username and avatar. If you call the standard REST endpoint (GET /users), the server doesn't know what you need. So, it sends back a massive JSON object for every single user containing their username, avatar, email, home address, phone number, date of birth, and account settings.

Why it's bad: You just downloaded 100 kilobytes of data when you only needed 5 kilobytes. For mobile users on weak 3G connections, this drains battery life, eats up data plans, and slows down the app significantly.
Look closely at the code block in the image. It looks almost exactly like a JSON object, but with the "values" missing. This is the Query Language.

Here is what that specific query is doing:

Pagination Variables: ($limit: Int = 10, $offset: Int = 0). This tells the server, "I don't want a million users, just give me the first 10."

The Graph Traversal: Notice how the data is nested. Inside users, it asks for profile. Inside profile, it asks for groups. And inside groups, it asks for category.

The Magic: Because the backend developer explicitly linked these tables together in the GraphQL schema, the frontend can infinitely traverse these relationships in a single network request without writing custom SQL joins or building brand new API endpoints.

GraphQL is a strongly typed language. Before a GraphQL server can run, you have to write a strict "Schema" (a contract).

GraphQL
type User {
  id: ID!
  username: String!
  age: Int!        # This MUST be an integer. The '!' means it cannot be null.
  isOnline: Boolean!
}

cons:
complexity
no caching
no standard errors
expensive queries backend




```

Rule of thumb for system design
Small filters/search parameters → GET
Large request data → POST
Don't assume 2048 is a universal limit.
The actual limit is usually determined by browsers, proxies, load balancers, and web servers—not HTTP itself.

```
One of the biggest reasons GET is preferred for reads is that it works very naturally with HTTP caching mechanisms like ETag, Cache-Control, and Last-Modified.

First request

Client sends:

GET /products/123

Server responds:

200 OK
ETag: "abc123"

{
  "id": 123,
  "name": "Laptop"
}

The browser caches both:

Response body
ETag value "abc123"
Second request

Later the browser asks again:

GET /products/123
If-None-Match: "abc123"

This means:

"I already have version abc123. Has it changed?"
```

