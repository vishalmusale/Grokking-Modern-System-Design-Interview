# Quiz on CDN's Design
```
1. Which CDN approach will be the most suitable to use when most of the web content is static?

A)
Pull CDN

B)
Push CDN
```

```
2. (Select all that apply.) What are the limitations of using a public CDN?

A)
An additional point of failure

B)
Risk of a data breach

C)
Loss of control

D)
An additional DNS lookup

E)
Increased latency
```

```
3. (Select all that apply.) What are the main reasons for building a specialized CDN?

A)
It optimizes the content delivery.

B)
It helps us avoid the increasing cost of CDN providers.

C)
It prevents ISP intervention.

D)
It reduces the hit ratio.
```

```
4. Suppose you’re asked to scale the Quora system to reduce the burden of data distribution on the origin server. Which technique will you use to do this?

A)
A single-tier CDN

B)
A multi-tier CDN

C)
A public CDN

D)
A multi CDN
```

```
5. (Select all that apply.) Why do most websites use a CDN?

A)
A CDN ensures improved scalability.

B)
A CDN offers protection against DDoS attacks.

C)
A CDN creates a backup for all the evicted content.

D)
A CDN reduces the load on the origin server.

E)
A CDN guarantees better performance.
```

```
6. Which metric pair is the most suitable for finding the nearest proxy servers?

A)
Traffic load, caching capacity

B)
Request load, network distance

C)
Location, bandwidth

D)
Caching capacity, network distance
```

Answers
```
1. Which CDN approach will be the most suitable to use when most of the web content is static? (B)

A)
Pull CDN

Explanation
Use Pull CDN where web content changes frequently.

Correct Answer
B)
Push CDN

Explanation
Use Push CDN where web content changes infrequently and caches in the edge proxy servers for a long period.
```

```
2. (Select all that apply.) What are the limitations of using a public CDN? (A)(B)(C)(D)

A)
An additional point of failure

Explanation
The content hosted on CDN will not be available.

B)
Risk of a data breach

Explanation
There are always risks when third parties manage the data.

C)
Loss of control

Explanation
When content publishes to the proxy servers, the CDN providers control it.

D)
An additional DNS lookup

Explanation
CDN network layer increases DNS lookup.

E)
Increased latency

Explanation
CDN is used to reduce the latency between end-users and the content. Therefore, this option can not be a limitation.
```

```
3. (Select all that apply.) What are the main reasons for building a specialized CDN? (A)(B)

A)
It optimizes the content delivery.

Explanation
Specified CDN is dedicated to a particular content provider which optimizes the delivery of the requested content.

B)
It helps us avoid the increasing cost of CDN providers.

Explanation
The cost of CDN providers increases when we increase the cache size or add more components.

C)
It prevents ISP intervention.

Explanation
Each request comes through ISP using encrypted connections. So, ISPs can’t intervene.

D)
It reduces the hit ratio.

Explanation
Specialized CDN will increase the hit ratio instead of reducing it because it is dedicated to particular content.
```

```
4. Suppose you’re asked to scale the Quora system to reduce the burden of data distribution on the origin server. Which technique will you use to do this? (B)

A)
A single-tier CDN

Explanation
Single tier does not reduce the burden because an origin server has to distribute the content to all CDN servers.

Correct Answer
B)
A multi-tier CDN

Explanation
Using this approach, data distribution is divided into the CDN layers like an origin to parent CDN servers and parent to the following layer CDN servers.

C)
A public CDN

Explanation
The origin server will need to provide data to CDN, be it public or private.

D)
A multi CDN

Explanation
A multi-CDN combines multiple CDNs from different CDN providers into a single network. Often such a strategy is complex and expensive.
```

```
5. (Select all that apply.) Why do most websites use a CDN? (A)(B)(D)(E)

A)
A CDN ensures improved scalability.

Explanation
Horizontal scaling is not a problem for the CDN.

B)
A CDN offers protection against DDoS attacks.

Explanation
Scrubber servers are used to prevent DDoS attacks in the CDN network.

C)
A CDN creates a backup for all the evicted content.

Explanation
Content is deleted from all storage of the specified CDN servers for consistency in the eviction process.

D)
A CDN reduces the load on the origin server.

Explanation
CDN reduces the burden from the origin servers like data distribution, handling massive traffic, etc.

E)
A CDN guarantees better performance.

Explanation
CDN is placed near the end-user, so it increases the performance by reducing latency and speeding up the request/response process.
```

```
6. Which metric pair is the most suitable for finding the nearest proxy servers? (B)

A)
Traffic load, caching capacity

Explanation
Caching capacity is not a relevant factor, but Traffic load is.

Correct Answer
B)
Request load, network distance

Explanation
This is the best suitable pair to find the nearest proxy server.

C)
Location, bandwidth

Explanation
Location does not describe any details, but the distance between two locations does.

D)
Caching capacity, network distance

Explanation
Caching capacity is not a relevant factor, but network distance is.
```
