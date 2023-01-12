# Quiz on YouTube's Design


1。Which pair of requirements among the following cannot be compromised if we’re asked to design Netflix?

A)
Low latency and high availability

B)
Low latency and HD video

C)
High availability and HD video

D)
Consistency and HD video



2。Consider the following design to upload content to the Netflix service:

[design](./design.jpg)

A.[A](./2A.jpg)

B.[B](./2B.jpg)

C.[C](./2C.jpg)

D.[D](./2D.jpg)


3 Which encoding technique is the most effective in terms of streaming to end users?

A)
Use a single encoding technique for all types of content to achieve simplicity in design.

B)
Encode the entire video based on the content inside it—for example, encode an action movie with dynamic colors differently than a 2D cartoon.

C)
Use different encoding techniques for different shots or segments within a video. For example, highly dynamic scenes should be encoded differently than lesser dynamic scenes within a single video.

D)
Encoding doesn’t matter at all.


4 Adaptive bitrate streaming is a common technique used to provide a good streaming experience to the user. It works by detecting a user’s bandwidth and the CPU capacity of the user’s device in real time, and adjusts the quality of the media stream accordingly.

Considering the above explanation, which diagram explains adaptive bitrate the best?

A.[A](./4A.jpg)

B.[B](./4B.jpg)

C.[C](./4C.jpg)

D.[D](./4D.jpg)

5. What is the most appropriate sequence from development to end user delivery to stream content?

A)
Encoding, bitrate conversion, subtitles addition, and deployment

B)
Deployment, bitrate conversion, subtitles, and encoding

C)
Encoding, bitrate conversion, uploading to CDN, and deployment

D)
Uploading to CDN, encoders, and bitrate conversion



6. Assume that 100,000 users try to watch a football stream at 1080p in a densely populated city. If the CDN point of presence (PoP) in that area can provide a bandwidth of 300 Gbps for end users, which design best serves the clients without any buffering issues?

A.[A](./6A.jpg)

B.[B](./6B.jpg)

C.[C](./6C.jpg)

D.[D](./6D.jpg)





Answers

1 Which pair of requirements among the following cannot be compromised if we’re asked to design Netflix?

Correct Answer
A)
Low latency and high availability

Explanation
Streaming services highly require these two design goals to provide a good QoE to end-user.

B)
Low latency and HD video

Explanation
It is extremely important for the service to be available even if the video is not high quality

C)
High availability and HD video

Explanation
This could lead to buffering and lag issues. Therefore, low latency is required.

D)
Consistency and HD video

Explanation
Consistency isn’t the most challenging or desired metric when it comes to streaming services.




2 Consider the following design to upload content to the Netflix service:



Note that there are two unnamed components. Select the correct option to complete the design.

A)

Explanation
Metadata storage cannot be the first point of contact for the end-users.

B)

Explanation
It doesn’t make sense for the uploading servers and Mapreduce to store data in colocation sites instead of a datastore.

Correct Answer
C)

Explanation
Users’ requests are distributed among uploading servers using load balancers. Also, we can use a datastore to save (meta)data from uploading servers and Mapreduce.

D)

Explanation
Web servers require load balancers before them in practical designs. Moreover, uploading servers would extract metadata from raw videos and store it in a database that isn’t a key-value store.






3 Which encoding technique is the most effective in terms of streaming to end users?

A)
Use a single encoding technique for all types of content to achieve simplicity in design.

Explanation
Depending on the type of content within a video, it is better to use different encoding schemes to get optimal results.

B)
Encode the entire video based on the content inside it—for example, encode an action movie with dynamic colors differently than a 2D cartoon.

Explanation
Encoding entire video helps but it is not the most optimal solution.

Correct Answer
C)
Use different encoding techniques for different shots or segments within a video. For example, highly dynamic scenes should be encoded differently than lesser dynamic scenes within a single video.

Explanation
Using a per-shot encoding technique can save storage space, transmission bandwidth, as well as make streaming convenient in terms of user bandwidth.

D)
Encoding doesn’t matter at all.

Explanation
This isn’t true. Encoding helps in the overall optimization.




4 Adaptive bitrate streaming is a common technique used to provide a good streaming experience to the user. It works by detecting a user’s bandwidth and the CPU capacity of the user’s device in real time, and adjusts the quality of the media stream accordingly.

Considering the above explanation, which diagram explains adaptive bitrate the best?

A)

Explanation
Webservers don’t generate multiple video qualities. It is the job of encoders.

Your Answer
B)

Explanation
CDNs don’t generate multiple video qualities. It is the job of encoders.

C)

Explanation
Application servers run the business or logic of the application instead of serving videos to the clients.

Correct Answer
D)


Explanation
The encoder converts videos into multiple formats and the streaming server sends it to the client.



5 What is the most appropriate sequence from development to end user delivery to stream content?

Correct Answer
A)
Encoding, bitrate conversion, subtitles addition, and deployment

B)
Deployment, bitrate conversion, subtitles, and encoding

Explanation
It is non-sensical to first deploy a video and then encode it.

C)
Encoding, bitrate conversion, uploading to CDN, and deployment

Explanation
Uploading to CDN is the same thing as deployment. Also, subtitles addition is missed out.

D)
Uploading to CDN, encoders, and bitrate conversion

Explanation
First, videos must be encoded and then deployed to CDNs.




6 Assume that 100,000 users try to watch a football stream at 1080p in a densely populated city. If the CDN point of presence (PoP) in that area can provide a bandwidth of 300 Gbps for end users, which design best serves the clients without any buffering issues?

A)

Explanation
Not the best choice because it will require an extraordinary bandwidth for the CDN to serve out 100,000 users each with 1080p quality of streaming service.

B)

Explanation
This strategy will put huge burden on the backbone Internet. Bottlenecks will create issues.

Correct Answer
C)

Explanation
Cache servers maintained at the ISP will provide coverage to all the users reducing bandwidth requirements for the CDN as well as the origin servers.

D)

Explanation
Streaming servers are an alternative to colocation sites. These will not be enough for 100,000 users within the same geographical location.
