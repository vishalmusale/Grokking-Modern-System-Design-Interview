# Evaluation of a Newsfeed System’s Design
## Fulfill requirements
Our non-functional requirements for the proposed newsfeed system design are scalability, fault tolerance, availability, and low latency. Let’s discuss how the proposed system fulfills these requirements:

1. Scalability: The proposed system is scalable to handle an ever-increasing number of users. The required resources, including load balancers, web servers, and other relevant servers, are added/removed on demand.

2. Fault tolerance: The replication of data consisting of users’ metadata, posts, and newsfeed makes the system fault-tolerant. Moreover, the redundant resources are always there to handle the failure of a server or its component.

3. Availability: The system is highly available by providing redundant servers and replicating data on them. When a user gets disconnected due to some fault in the server, the session is re-created via a load balancer with a different server. Moreover, the data (users metadata, posts, and newsfeeds) is stored on different and redundant database clusters, which provides high availability and durability.

4. Low latency: We can minimize the system’s latency at various levels by:
  - Geographically distributed servers and the cache associated with them. This way, we bring the service close to users.
  - Using CDNs for frequently accessed newsfeeds and media content.

## Quiz on the newsfeed system’s design
Test your understanding of the concepts related to the design of the newsfeed system with a quiz.

```
1 Which component is responsible for storing relationships between users, their friends, and followers?

A)
The users database

B)
The graph database

C)
The posts database

D)
None of the above
```

```
2 Where are fully constructed and ranked newsfeeds stored?

A)
The published feeds cache

B)
The newsfeed cache

C)
The posts cache

D)
None of the above
```

```
3 When do the web servers call the posts service?

A)
When new posts are created

B)
When a request for a newsfeed is received

C)
When users are to be notified due to some failure events

D)
All of the above
```
```
4 Which option below is stored in blob storage?

A)
Comments on posts

B)
Count of likes and dislikes

C)
Media content

D)
All of the above
```

Answers
1. (B)

2. (B)

3. (A)

4. (C)

## Summary
In this chapter, we learned to design a newsfeed system at scale. Our design ranked enormous user data to show carefully curated content to the user for better user experience and engagement. Our newsfeed design is general enough that it can be used in many places such as Twitter feeds, Facebook posts, YouTube and Instagram recommendations, News applications, and so on.
