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
Let’s keep in mind our assumption that 15% of questions have images and 5% have videos. So, we’ll make the following assumptions to estimate the storage requirements for our design:

- Each of the 300 million active users posts 1 question in a day, and each question has 2 responses on average, 10 upvotes, and 5 comments in total.
- The collective storage required for the textual content of one question equals 1 KB.

```
    Storage Requirements Estimation Calculator
             
Questions per user                    	1	per day

Total questions per day	                300	millions

Size of textual content per question  	1	KB

Image size                            	250	KB

Video size	                            5 	MB

Questions containing images	            15	percent

Questions containing videos           	5	percent

Storage for textual content	            0.3	TB

Storage for image content	              11.25	TB

Storage for video content	              75	TB                           

```

```
The following are the default calculations:

- Total questions: 300M×1=300×10^6 questions per day.
- Storage required for textual content of all questions in one day: 300×M×1×KB=300GB
- Storage required for images for one day: (300 x 10^6 x 15)/100 x 250 x 10^3 B = 11.25TB
- Storage required for video content for one day: (300 x 10^6 x 15)/100 x 5 x 10^6 B= 75TB
```
Total storage required for one day = 0.3TB + 11.25TB + 75TB ~= 86.55TB per day

The daily storage requirements of Quora seem very high. But for service with 300 million DAU, a yearly requirement of 86.55TB \times 365 = 31.6PB
86.55TB×365=31.6PB is feasible. The practical requirement will be much higher because we have disregarded the storage required for a number of things. For example, non-active (out of 1B) users’ data will require storage.

### Bandwidth estimation
The bandwidth estimate requires the calculation of incoming and outgoing data through the network.

- Incoming traffic: The incoming traffic bandwidth required per day will be equal to 86.55TB /86400 ×8=8Gbps
- Outgoing traffic: We have assumed that 300 million active users views 20 questions per day, so the total bandwidth requirements can be found in the below calculator:

```
    Bandwidth Requirements Estimation Calculator
Total storage required per day	          86.55	TB

Incoming traffic bandwidth	              8	Gbps

Questions viewed per user	                20	per day

Total questions viewed	                  69444	per second

Bandwidth for text of all questions	      0.56	Gbps

Bandwidth for 15% of image content	      20.83	Gbps

Bandwidth for 5% of video content	        138.89	Gbps

Outgoing traffic bandwidth	              160.3	Gbps                     

```

```
300M×20 questions=6 billion questions are viewed per day.
- Questions viewed per second: 6 x 10^9/86400 ~= 69.4 x 10^3 questions are viewed per second.
- Bandwidth for the textual content of all questions and their answers: 69.4 x 10^3 x 1 x 10^3 x 8 bits = 0.56 Gbps
- Bandwidth of the 15% of content which contain images per second: 69.4 x 10^3 x 15/100 x 250 x 10^3 x 8 bits = 20.82Gbps
- Bandwidth for the 5% of content that contains video per second: 69.4 x 10^3 x 5/100 x 5 x 10^6 x 8 bits = 138.9Gbps
- Total outgoing traffic bandwidth: 0.56Gbps + 20.82Gbps + 138.9Gbps = 160.3Gbps
We use rounding at each step in this explanation. The answers in the calculator above are slightly different due to rounding.
```

[Summarizing the bandwidth requirements of Quora]

Total bandwidth requirement of Quora is equal to:

```
Incoming + outgoing traffic bandwidth = 8Gbps + 160.3Gbps = 168.3Gbps
```


## Building blocks we will use
We’ll use the following building blocks for the initial design of Quora:

[Building blocks required for our design]

- Load balancers will be used to divide the traffic load among the service hosts.
- Databases are essential for storing all sorts of data, such as user questions and answers, comments, and likes and dislikes. Also, user data will be stored in the databases. We may use different types of databases to store different data.
- A distributed caching system will be used to store frequently accessed data. We can also use caching to store our view counters for different questions.
- The blob store will keep images and video files.
