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
