# Design of YouTube
## High-level design
The high-level design shows how we’ll interconnect the various components we identified in the previous lesson. We have started developing a solution to support the functional and non-functional requirements with this design.

[The high-level design of YouTube]

The workflow for the abstract design is provided below:

1. The user uploads a video to the server.
2. The server stores the metadata and the accompanying user data to the database and, at the same time, hands over the video to the encoder for encoding (see 2.1 and 2.2 in the illustration above).
3. The encoder, along with the transcoder, compresses the video and transforms it into multiple resolutions (like 2160p, 1440p, 1080p, and so on). The videos are stored on blob storage (similar to GFS or S3).
4. Some popular videos may be forwarded to the CDN, which acts as a cache.
5. The CDN, because of its vicinity to the user, lets the user stream the video with low latency. However, CDN is not the only infrastructure for serving videos to the end user, which we will see in the detailed design.

```
Question
Why don’t we upload the video directly to the encoder instead of to the server? Doesn’t the current strategy introduce an additional delay?

Answer
There are several reasons why it’s a good idea to introduce a server in between the encoder and the client:

- The client could be malicious and could abuse the encoder.
- If the uploaded video is a duplicate, the server could filter it out.
- Encoders will be available on a private IP address within YouTube’s network and not available for public access.
```

## API design
Let’s understand the design of APIs in terms of the functionalities we’re providing. We’ll design APIs to translate our feature set into technical specifications. In this case, REST APIs can be used for simplicity and speed purposes. Our API design section will help us understand how the client will request services from the back-end application of YouTube. Let’s develop APIs for each of the following features:

- Upload videos
- Stream videos
- Search videos
- View thumbnails
- Like or dislike videos
- Comment on videos

[API design overview]

### Upload video
The POST method can upload a video to the /uploadVideo API:
```
uploadVideo(user_id, video_file, category_id, title, description, tags, default_language, privacy_settings)
```
Let’s take a look at the description of the following parameters here.
```
Parameter              Description

user_id                This is the user that is uploading the video.

video_file             This is the video file that the user wants to upload.

category_id            This refers to the category a video belongs to. Typical categories can be “Entertainment,” “Engineering,” “Science,” and so on.

title                  This is the title of the video.

description            This is the description of the video.

tags                   This refers to the specific topics the content of the video covers. The tags can improve search results.

default_language       This is the default language a page will show to the user when the video is streamed.

privacy_settings       This refers to the privacy of the video. Generally, videos can be a public asset or private to the uploader.
```


### Stream video
### Search videos
### View thumbnails
### Like and dislike a video
### Comment video
## Storage schema
## Detailed design
### Detailed design components
### Design flow and technology usage
## YouTube search
