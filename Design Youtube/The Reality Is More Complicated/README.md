# The Reality Is More Complicated
## Introduction
Now that we’ve understood the design well, let’s see how YouTube can optimize the usage of storage and network demands while maintaining good quality of experience (QoE) for the end user.

When talking about providing effective service to end users, the following three steps are important:

- Encode: The raw videos uploaded to YouTube have significant storage requirements. It’s possible to use various encoding schemes to reduce the size of these raw video files. Apart from compression, the choice of encoding scheme will also depend on the types of end devices used to stream the video content. Since multiple devices could be used to stream the same video, we may have to encode the same video using different encoding schemes resulting in one raw video file being converted into multiple files each encoded differently. This strategy will result in a good user-perceived experience because of two reasons: users will save bandwidth because the video file will be encoded and compressed to some limit, and the encoded video file will be appropriate for the client for a smooth playback experience.
- Deploy: For low latency, content must be intelligently deployed so that it is closer to a large number of end users. Not only will this reduce latency, but it will also put less burden on the networks as well as YouTube’s core servers.
- Deliver: Delivering to the client requires knowledge about the client or device used for playing the video. This knowledge will help in adapting to the client and network conditions. Therefore, we’ll enable ourselves to serve content efficiently.

Let’s understand each phase in detail now.

## Encode
Until now, we’ve considered encoding one video with different encoding schemes. However, if we encode videos on a per-shot basis, we’ll divide the video into smaller time frames and encode them individually. We can divide videos into shorter time frames and refer to them as segments. Each segment will be encoded using multiple encoding schemes to generate different files called chunks. The choice of encoding scheme for a segment will be based on the detail within the segment to get optimized quality with lesser storage requirements. Eventually, each shot will be encoded into multiple chunk sizes depending on the segment’s content and encoding scheme used. As we divide the raw video into segments, we’ll see its advantages during the deployment and delivery phase.

Let’s understand how the per-segment encoding will work. For any video with dynamic colors and high depth, we’ll encode it differently from a video with fewer colors. This means that a not-so-dynamic segment will be encoded such that it’s compressed more to save additional storage space. Eventually, we’ll have to transfer smaller file sizes and save bandwidth during the deployment and streaming phases.

[Higher quality requiring higher bitrate from left to right]

Using the strategy above, we’ll have to encode individual shots of a video in various formats. However, the alternative to this would be storing an entire video (using no segmenting) after encoding it in various formats. If we encode on a per-shot basis, we would be able to optimally reduce the size of the entire video by doing the encoding on a granular level. We can also encode audio in various formats to optimally allow streaming for various clients like TVs, mobile phones, and desktop machines. Specifically, for services like Netflix, audio encoding is more useful because audios are offered in various languages.

[A raw video file being encoded into different formats including its audio and subtitles]

## Deploy
As discussed in our design and evaluation sections, we have to bring the content closer to the user. This has three main advantages:

1. Users will be able to stream videos quickly.
2. There will be a reduced burden on the origin servers.
3. Internet service providers (ISPs) will have spare bandwidth.
So, instead of streaming from our data centers directly, we can deploy chunks of popular videos in CDNs and point of presence (PoPs) of ISPs. In places where there is no collaboration possible with the ISPs, our content can be placed in internet exchange point (IXPs). We can put content in IXPs that will not only be closer to users, but can also be helpful in filling the cache of ISP PoPs.

[Streaming from data center to users through IXP and ISPs]

We should keep in mind that the caching at the ISP or IXP is performed only for the popular content or moderately popular content because of limited storage capacity. Since our per-shot encoding scheme saves storage space, we’ll be able to serve out more content using the cache infrastructure closer to end users.

Additionally, we can have two types of storage at the origin servers:

1. Flash servers: These servers hold popular and moderately popular content. They are optimized for low-latency delivery.
2. Storage servers: This type holds a large portion of videos that are not popular. These servers are optimized to hold large storage.

```
Note: When we transfer streaming content, it can result in the congestion of networks. That is why we have to transfer the content to ISPs in off-peak hours.
```

### Recommendations
Recommendations
YouTube recommends videos to users based on their profile, taking into account factors such as their interests, view and search history, subscribed channels, related topics to already viewed content, and activities on content such as comments and likes.

An approximation of the recommendation engine of YouTube is provided below. YouTube filters videos in two phases:

1. Candidate generation: During this phase, millions of YouTube videos are filtered down to hundreds based on the user’s history and current context.
2. Ranking: The ranking phase rates videos based on their features and according to the user’s interests and history. Hundreds of videos are filtered and ranked down to a few dozen videos during this phase.
YouTube employs machine learning technology in both phases to provide recommendations to users.

```
Covington, Paul, Jay Adams, and Emre Sargin. “Deep neural networks for youtube recommendations.” Proceedings of the 10th ACM conference on recommender systems. 2016.
```

[YouTube's recommendation engine using two neural networks to filter videos from millions to dozens]

```
Question 1
Previously, we said that popular content is sent to ISPs, IXPs, and CDNs. We’ve now discussed YouTube’s feature that recommends content. What is the difference between popular and recommended content on YouTube?

Answer
Recommendations are specific to users’ profiles and interests, whereas popular content is recognized on a regional or global basis. It is possible to present popular content to the general audience.
```

```
Question 2
Can you provide some formulaic representation of how the YouTube algorithm for popular content would work?

Answer
To approximate a formula, we can assume a threshold value which is the weighted sum of all the considered factors like this:

Th reg =Comments wt × Comments num +Likes wt ×Likes num +Links wt ×Links num ⋯

Where

Th_{reg} is the number that will be used to decide whether a video is viral in a specific region.
Comments_{wt} is the weight of the comments.
Comments_{num} is the number of comments.
Likes_{wt} is the weight of likes.
Likes_{num} is the number of likes.
Links_{wt} is the weight of the links.
Links_{num} is the number of links.

The cumulative sum of each weight is equal to 1.

We may also assume that different threshold levels can be considered for different regions. Finally, we can consider a video to be globally popular if the sum of thresholds of different regions passes a global threshold value. YouTube may also decide to put some videos directly in CDN depending on the channel used to upload the videos.
```

```
Question 3
In reference to Question 2, how often do you think that the approximation calculation for whether content is popular will be made? On each click, like, or comment?

Answer
Calculation per click, like, or comment requires special infrastructure to perform calculations correctly and in real-time. This should be limited to:

The most popular channels.
Alternatively, a particular metric that triggers the computation every time it crosses a certain value. A good trigger could be an increasing number of requests made for a specific video in a shorter period of time.
```

## Deliver
Let’s see how the end user gets the content on their device. Since we have the chunks of videos already deployed near users, we redirect users to the nearest available chunks. As shown below, whenever a user requests content that YouTube has recognized as popular, YouTube redirects the user to the nearest CDN.

However, in the case of non-popular content, the user is served from colocation sites or YouTube’s data center where the content is stored initially. We have already learned how YouTube can reduce latency times by having distributed caches at different design layers.

### Adaptive streaming
## Potential follow-up questions
