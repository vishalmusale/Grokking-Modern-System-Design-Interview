# Requirements of Quora's Design
## Requirements
Let’s understand the functional and non-functional requirements below:

### Functional requirements
A user should be able to perform the following functionalities:

- Questions and answers: Users can ask questions and give answers. Questions and answers can include images and videos.
- Upvote/downvote and comment: It is possible for users to upvote, downvote, and comment on answers.
- Search: Users should have a search feature to find questions already asked on the platform by other users.
- Recommendation system: A user can view their feed, which includes topics they’re interested in. The feed can also include questions that need answers or answers that interest the reader. The system should facilitate user discovery with a recommender system.
- Ranking answers: We enhance user experience by ranking answers according to their usefulness. The most helpful answer will be ranked highest and listed at the top.

[Functional and non-functional requirements of Quora]

### Non-functional requirements
- Scalability: The system should scale well as the number of features and users grow with time. It means that the performance and usability should not be impacted by an increasing number of users.
- Consistency: The design should ensure that different users’ views of the same content should be consistent. In particular, critical content like questions and answers should be the same for any collection of viewers. However, it is not necessary that all users of Quora see a newly posted question, answer, or comment right away.
- Availability: The system should have high availability. This applies to cases where servers receive a large number of concurrent requests.
- Performance: The system should provide a smooth experience to the user without a noticeable delay.

## Resource estimation
In this section, we’ll make an estimate about the resource requirements for Quora service. We’ll make assumptions to get a practical and tractable estimate. We’ll estimate the number of servers, the storage, and the bandwidth required to facilitate a large number of users.

Assumptions: It is important to base our estimation on some underlying assumptions. We, therefore, assume the following:

- There are a total of 1 billion users, out of which 300 million are daily active users.
- Assume 15% of questions have an image, and 5% of questions have a video embedded in them. A question cannot have both at the same time.
- We’ll assume an image is estimated to be 250 KBs, and a video is considered 5 MBs.

### Number of servers estimation
Let’s estimate our requests per second (RPS) for our design. If there are an average of 300 million daily active users and each user can generate 20 requests per day, then the total number of requests in a day will be:

300 x 10^6 x 20= 6 x 10^9

Therefore, the RPS = 6 x 10^9/86400 = 69500 approximately requests per second.
```
                    Estimating RPS

Daily active users	300	million

Requests per day per user	20

Requests Per Second (RPS)	69444
```

We already established in the back-of-the-envelope calculations chapter that we’ll use the following formula to estimate a pragmatic number of servers:

Number of daily active users/ RPS of a server= 300 x 10^6/8000=37500

[The estimated number of servers required for Quora]

```
Therefore, the total number of servers required to facilitate 300 million users generating an average of 69,500 requests per second will be 37,500.
```

### Storage estimation
### Bandwidth estimation
## Building blocks we will use
