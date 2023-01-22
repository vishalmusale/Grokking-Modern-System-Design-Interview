# System Design: Instagram
## What is Instagram?
Instagram is a free social networking application that allows users to post photos and short videos. Users can add a caption for each post and utilize hashtags or location-based geotags to index them and make them searchable within the application. A user’s Instagram posts display in their followers’ feeds and can be seen by the general public if they are tagged with hashtags or geotags. Alternatively, users can choose to make their profile private, which limits access to those who have chosen to follow them.

The expansion in the number of users requires more resources (servers, databases, and so on) over time. Knowing the users’ growth rate helps us predict the resources to scale our system accordingly. The following illustration shows the Instagram user base in different countries as of January 2022 (source: Statista).

[Countries with the most Instagram users](./countries.jpg)

## How will we design Instagram?
We have divided the design of Instagram into four lessons:

1. Requirements: This lesson will put forth the functional and non-functional requirements of Instagram. It will also estimate the resources required to achieve these requirements.
2. Design: This lesson will explain the workflow and usage of each component, API design and database schema.
3. Detailed design: In this lesson, we’ll explore the components of our Instagram design in detail and discuss various approaches to generate timelines. Moreover, we’ll also evaluate our proposed design.
4. Quiz: This lesson will test our understanding of the Instagram design.
Let’s start by understanding the requirements for designing our Instagram system and provide resource estimations in the next lesson.
