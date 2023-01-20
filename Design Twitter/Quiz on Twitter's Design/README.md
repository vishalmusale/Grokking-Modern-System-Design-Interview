# Quiz on Twitter's Design
```
1 Suppose you work as an engineer at a well-known company providing social services. Your task is to improve real-time event processing to get frequent results. Which tool below will help you the most in this scenario?

A)
BigQuery

B)
Apache Kafka

C)
Vertica

D)
FlockDB
```

```
2 Assume that an account of a public figure with millions of followers posts a Tweet on Twitter. Your system will need to handle millions of interactions with this Tweet by the account’s millions of followers. Which solution below is the best way to handle this traffic, assuming that the system knows the audience details of the Tweet?

A)
Dedicate a few servers to the public figure in the central data center(s).

B)
Increase or dedicate some servers to particular locations where a large portion of the audience belongs.

C)
Increase the number of servers in all Twitter’s data centers situated in different regions to handle massive traffic.

D)
Show the Tweet to followers region-wise to avoid handling massive traffic.
```

```
3 When the user sends a home timeline request, the system responds with a specified number of Top-k tweets to the user. On what basis does the system identify the Top-k tweets for a particular user?

A)
The user liked the Tweets (posted by the unfollowed account) and Trends.

B)
The user’s followers and location.

C)
The user’s followed accounts’ Tweets and Retweeted Tweets by the followed accounts.

D)
Location and unfollowed accounts
```

```
4 Sharded counters are an efficient solution to count multiple interactions (like or view) on thousands of celebrities’ Tweets individually. The problem is that when the user interacts with any Tweet, it needs an immediate response (for instance, an increase or decrease in the like count). Which solution below will help in this regard?

A)
Maintain counters in the server cache.

B)
Place specified shards of the particular counters near the end users based on the celebrity’s history (Last few Tweets’ audiences).

C)
Increase the number of shards of multiple counters that belong to the Tweet in the central data center.

D)
Create a real-time counter in the client cache with the specified detail of the Tweet.
```

```
5 (Select all that apply.) We discussed how the client-side load balancers work and what kind of benefit it provides. Which of the options below were identified as possible drawbacks of client-side load balancers?

A)
They act as a single point of failure.

B)
They’re not suitable for small-scale applications because there are no dedicated servers for the services.

C)
They increase network hop.

D)
They make it more difficult to update all clients when servers add/drop or algorithm modify.
```

Answers

```
1
Suppose you work as an engineer at a well-known company providing social services. Your task is to improve real-time event processing to get frequent results. Which tool below will help you the most in this scenario?

A)
BigQuery

Explanation
BigQuery is a serverless, fully managed data warehouse that allows for scalable analysis of vast amounts of data.

Correct Answer
B)
Apache Kafka

Explanation
Apache Kafka is a framework for distributed real-time event processing and storage.

C)
Vertica

Explanation
Vertica is a columnar data storage that can manage massive amounts of data and provides lightning-fast query performance in usually time-consuming circumstances.

D)
FlockDB

Explanation
FlockDB is a distributed, fault-tolerant graph database for handling large network graphs.
```


```
2
Assume that an account of a public figure with millions of followers posts a Tweet on Twitter. Your system will need to handle millions of interactions with this Tweet by the account’s millions of followers. Which solution below is the best way to handle this traffic, assuming that the system knows the audience details of the Tweet?

A)
Dedicate a few servers to the public figure in the central data center(s).

Explanation
Increase burden on central data center and also increase latency.

Correct Answer
B)
Increase or dedicate some servers to particular locations where a large portion of the audience belongs.

C)
Increase the number of servers in all Twitter’s data centers situated in different regions to handle massive traffic.

Explanation
If most of the traffic is coming from a few regions, increasing servers in other datacenters is useless and resource wastage.

D)
Show the Tweet to followers region-wise to avoid handling massive traffic.

Explanation
All users having connections with tweets must get the tweet. So, it is not fulfilling the service.
```


```
3
When the user sends a home timeline request, the system responds with a specified number of Top-k tweets to the user. On what basis does the system identify the Top-k tweets for a particular user?

A)
The user liked the Tweets (posted by the unfollowed account) and Trends.

Explanation
Trends metric is irrelevant here.

B)
The user’s followers and location.

Explanation
Users will not get the tweets posted by their followers.

Correct Answer
C)
The user’s followed accounts’ Tweets and Retweeted Tweets by the followed accounts.

D)
Location and unfollowed accounts

Explanation
Users will not get unfollowed accounts’ tweets as long as tweets are not promoted.
```


```
4
Sharded counters are an efficient solution to count multiple interactions (like or view) on thousands of celebrities’ Tweets individually. The problem is that when the user interacts with any Tweet, it needs an immediate response (for instance, an increase or decrease in the like count). Which solution below will help in this regard?

A)
Maintain counters in the server cache.

Explanation
It is difficult to manage millions of counters in the cache because they are limited in size (memory).

Correct Answer
B)
Place specified shards of the particular counters near the end users based on the celebrity’s history (Last few Tweets’ audiences).

Explanation
In this case, the nearest server will immediately respond to the end-users who liked or viewed the tweet.

C)
Increase the number of shards of multiple counters that belong to the Tweet in the central data center.

Explanation
It will increase latency because central data centers are distant from the end-users and also increase the central servers’ burden.

D)
Create a real-time counter in the client cache with the specified detail of the Tweet.

Explanation
This solution has multiple problems, such as limited client cache. For instance, if the end-user performs many operations (like, view, reply) on many tweets, creating and managing many counters in the cache is difficult. Second, what if the client liked a post and the relevant counter is incremented in the client cache. But somehow client cache gets empty (due to any failure) before moving that details to the application server. So, this solution is not reliable.
```


```
5
(Select all that apply.) We discussed how the client-side load balancers work and what kind of benefit it provides. Which of the options below were identified as possible drawbacks of client-side load balancers?

A)
They act as a single point of failure.

Selected Option
B)
They’re not suitable for small-scale applications because there are no dedicated servers for the services.

Explanation
Each service is managed within the backend server. Therefore, no such type of communication (server selection service to service) is required among the server.

C)
They increase network hop.

Selected Option
D)
They make it more difficult to update all clients when servers add/drop or algorithm modify.
```
