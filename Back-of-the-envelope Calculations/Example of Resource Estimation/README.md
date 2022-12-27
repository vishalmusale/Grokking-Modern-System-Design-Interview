# Examples of Resource Estimation

## Introduction
Now that we’ve set the foundation for resource estimation, let’s make use of our background knowledge to estimate resources like servers, storage, and bandwidth. Below, we consider a scenario and a service, make assumptions, and based on those assumptions, we make estimations. Let’s jump right in!

## Number of servers required
Let’s make the following assumptions about a Twitter-like service.

There are 500 million (M) daily active users (DAU).

A single user makes 20 requests per day on average.

Recall that a single server can handle 8,000 RPS.

```
Total requests per second 500M x 20/86400=115K requests per second which is the RPS for our system.

For the number of servers, (Number of Request/sec) / RPS of server=115k/8k = 15  servers to handle all requests.

```

[Estimation of Number of Servers](./estimating_the_number_of_servers.jpg)

Indeed, the number above doesn’t seem right. If we only need 15 commodity servers to serve 500M daily users, then why do big services use millions of servers in a data center? The primary reason for this is that the RPS is not enough to estimate the number of servers required to provide a service. Also, we made some underlying assumptions in the calculations above. One of the assumptions was that a request is handled by one server only. In reality, requests go through to web servers that may interact with application servers that may also request data from storage servers. Each server may take a different amount of time to handle each request. Furthermore, each request may be handled differently depending upon the state of the data center, the application, and the request itself. Remember that we have a variety of servers for providing various services within a data center.

Therefore, we approximate the number of servers by depicting how many clients a server handles on a given day:
In this case, it’s equal to 500M / 8000 = 62,500

```
Note: This may not be an accurate estimation, but it’s a realistic one. Therefore, we use this approach in estimating the number of servers in our design problems. Informally, the equation given above assumes that one server can handle 8,000 users. We use this reference in the rest of the course as well.
```

## Storage requirements

In this section, we attempt to understand how storage estimation is done by using Twitter as an example. We estimate the amount of storage space required by Twitter for new tweets in a year. Let’s make the following assumptions to begin with:
```
We have a total of 250 M daily active users.

Each user posts three tweets in a day.

Ten percent of the tweets contain images, whereas five percent of the tweets contain a video. Any tweet containing a video will not contain an image and vice versa.

Assume that an image is 200 KB and a video is 3 MB in size on average.

The tweet text and its metadata require a total of 250 Bytes of storage in the database.
```

Then, the following storage space will be required:

[Estimation of Storage Requirements](./estimating_storage_req.jpg)

```
Total tweets: 250M×3 = 750M x10^6 tweets per day
torage required for tweets in one day: 750 x 10 ^6 x 250 B = 187.5 GB
Storage required for 10 percent images for one day: (750 x 10^6 x 10/100) x 200 x 10^3B=15TB
Storage required for 5 percent video content for one day:(750 x 10^6 x 10/100) x 200 x 10^6B=112.5TB
```

```
Total storage required for one day = 0.1875 TB + 15 TB + 112.5 TB = approximately 128TB
Storage required for one year = 365 x 128 TB = 46.72 PB
```
[Total Storage of Twittter for 1 year](./total_storage_yearly.jpg)


## Bandwidth requirements

In order to estimate the bandwidth requirements for a service, we use the following steps:

Estimate the daily amount of incoming data to the service.

Estimate the daily amount of outgoing data from the service.

Estimate the bandwidth in Gbps (gigabits per second) by dividing the incoming and outgoing data by the number of seconds in a day.

### Incoming traffic: Let’s continue from our previous example of Twitter, which requires 128 TBs of storage each day. Therefore, the incoming traffic should support the following bandwidth per second:
```
128 x 10^12 / 86400 x8 = approximately 12Gbps
```

```
Note: We multiply by 8 in order to convert Bytes(B) into bits(b) because bandwidth is measured in bits per second.
```

### Outgoing traffic: Assume that a single user views 50 tweets in a day. Considering the same ratio of five percent and 10 percent for videos and images, respectively, for the 50 tweets, 2.5 tweets will contain video content whereas five tweets will contain an image. Considering that there are 250 M active daily users, we come to the following estimations:

[Estimating Bandwidth Requirements](./estimating_bandwidth_req.jpg)

```
250M×50 tweets=12.5 billion tweets are viewed per day
Tweets viewed per second: 12.5/86400 =145x 10^3 tweets per second
Bandwidth for tweet: 145 x 10^3 x 250 x 8 bits = approximately 0.3Gbps  (One tweet is equal to 250 bytes).
Bandwidth of 10 percent images in tweets in a second: 145 x 10^3 x 10/100 x 200 x 10^3 x 8 bits = 23.2 Gbps
Bandwidth for 5 percent video tweets in a second: 145x 10^3 x 5/100 x3 x10^6 x 8 bits = 174 Gbps

The total outgoing traffic required will be equal to: 0.3 + 23.2 + 174 =approx 197.5 Gbps.

```
Twitter will need a total of 12 Gbps of incoming traffic and 197.5 Gbps of outgoing, assuming that the uploaded content is not compressed. Total bandwidth requirements = 12 + 197.5 =209.5 Gbps
```

[The total bandwidth required by Twitter](./total_bandwidth.jpg)
