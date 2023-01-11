# Requirements of YouTube's Design
## Requirements
Let’s start with the requirements for designing a system like YouTube.

### Functional requirements
We require that our system is able to perform the following functions:

1. Stream videos
2. Upload videos
3. Search videos according to titles
4. Like and dislike videos
5. Add comments to videos
6. View thumbnails

[Representation of the functional and non-functional requirements]

### Non-functional requirements
It’s important that our system also meets the following requirements:

- High availability: The system should be highly available. High availability requires a good percentage of uptime. Generally, an uptime of 99% and above is considered good.
- Scalability: As the number of users grows, these issues should not become bottlenecks: storage for uploading content, the bandwidth required for simultaneous viewing, and the number of concurrent user requests should not overwhelm our application/web server.
- Good performance: A smooth streaming experience leads to better performance overall.
- Reliability: Content uploaded to the system should not be lost or damaged.
We don’t require strong consistency for YouTube’s design. Consider an example where a creator uploads a video. Not all users subscribed to the creator’s channel should immediately get the notification for uploaded content.

To summarize, the functional requirements are the features and functionalities that the user will get, whereas the non-functional requirements are the expectations in terms of performance from the system.

Based on the requirements, we’ll estimate the required resources and design of our system.

## Resource estimation
Estimation requires the identification of important resources that we’ll need in the system.

Hundreds of minutes of video content get uploaded to YouTube every minute. Also, a large number of users will be streaming content at the same time, which means that the following resources will be required:

- Storage resources will be needed to store uploaded and processed content.
- A large number of requests can be handled by doing concurrent processing. This means web/application servers should be in place to serve these users.
- Both upload and download bandwidth will be required to serve millions of users.
To convert the above resources into actual numbers, we assume the following:

- Total number of YouTube users: 1.5 billion.
- Active daily users (who watch or upload videos): 500 million.
- Average length of a video: 5 minutes.
- Size of an average (5 minute-long) video before processing/encoding (compression, format changes, and so on): 600 MB.
- Size of an average video after encoding (using different algorithms for different resolutions like MPEG-4 and VP9): 30 MB.

### Storage estimation
To find the storage needs of YouTube, we have to estimate the total number of videos and the length of each video uploaded to YouTube per minute. Let’s consider that 500 hours worth of content is uploaded to YouTube in one minute. Since each video of 30 MB is 5 minutes long, we require 30/5 = 6 MB to store 1 minute of video.

Let’s put this in a formula by assuming the following:

Total_{storage} : Total storage requirement.

Total_{upload/min} : Total content uploaded (in minutes) per minute.

- Example: 500 hours worth of video is uploaded in one minute.
Storage_{min} : Storage required for each minute of content

Then, the following formula is used to compute the storage:

Total_{storage} = Total_{upload/min} x Storage_{min} 

Below is a calculator to help us estimate our required resources. We’ll look first at the storage required to persist 500 hours of content uploaded per minute, where each minute of video costs 6 MBs to store:

```
                            Storage Required for Storing Content per Minute on YouTube
                            
No. of video hours per minute                 	Minutes per hour	              MB per minute                	Storage per minute (GB)    
500                                                 60                               6                           180

```

```
Try changing the values of Hours and MB per minute to see their impact on storage space requirements.
```

The numbers mentioned above correspond to the compressed version of videos. However, we need to transcode videos into various formats for reasons that we will see in the coming lessons. Therefore, we’ll require more storage space than the one estimated above.

[Total storage required by YouTube in a year]

```
Question
Assuming YouTube stores videos in five different qualities and the average size of a one-minute video is 6 MB, what would the estimated storage requirements per minute be?

Answer
Since we need 6 MBs per minute and we need to store files in five different formats, the overall requirement is 5×6MB=30 MBs.

Next, we’ll calculate the below value: 

Number of hours uploaded to Youtube/min x Number of minutes per hour x storage requirement per minute= 500 hours/ minute x 60 minutes/hour x 30 MB/minute = 900 GB/minute


### Bandwidth estimation
### Number of servers estimation
## Building blocks we will use
