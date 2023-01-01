# System Design: A Blob Store
## What is a blob store?
Blob store is a storage solution for unstructured data. We can store photos, audio, videos, binary executable codes, or other multimedia items in a blob store. Every type of data is stored as a blob. It follows a flat data organization pattern where there are no hierarchies, that is, directories, sub-directories, and so on.

Mostly, it’s used by applications with a particular business requirement called write once, read many (WORM), which states that data can only be written once and that no one can change it. Just like in Microsoft Azure, the blobs are created once and read many times. Additionally, these blobs can’t be deleted until a specified interval, and they also can’t be modified to protect critical data.
```
A blob (binary large object) consists of a collection of binary data stored as a single unit.
```

```
Note: It isn’t necessary for all applications to have this WORM requirement. However, we are assuming that the blobs that are written can’t be modified. Instead of modifying, we can upload a new version of a blob if needed.
```
## Why do we use a blob store?
Blob store is an important component of many data-intensive applications, such as YouTube, Netflix, Facebook, and so on. The table below displays the blob storage used by some of the most well-known applications. These applications generate a huge amount of unstructured data every day. They require a storage solution that is easily scalable, reliable, and highly available, so that they can store large media files. Since the amount of data continuously increases, these applications need to store an unlimited number of blobs. According to some estimates, YouTube requires more than a petabyte of additional storage per day. In a system like YouTube, a video is stored in multiple resolutions. Additionally, the video in all resolutions is replicated many times across different data centers and regions for availability purposes. That’s why the total storage required per video is not equal to the size of the uploaded video.
```
System          Blob Store

Netflix          S3

YouTube         Google Cloud Storage

Facebook         Tectonic
```

## How do we design a blob store system?
We have divided the design of the blob store into five lessons and a quiz.

1. Requirements: In this lesson, we identify the functional and non-functional requirements of a blob store. We also estimate the resources required by our blob store system.
2. Design: This lesson presents us with a high-level design, the API design, and a detailed design of the blob store, while explaining the details of all the components and the workflow.
3. Design considerations: In this lesson, we discuss some important aspects of design. For example, we learn about the database schema, partitioning strategy, blob indexing, pagination, and replication.
4. Evaluation: In this lesson, we evaluate our blob store based on our requirements.
5. Quiz: In this lesson, we assess understanding of the blob store design.
Let’s start with the requirements of a blob store system.
