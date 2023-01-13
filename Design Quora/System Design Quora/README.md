# System Design: Quora
## Introduction
With so much information available online, finding answers to questions can be daunting. That’s why information sharing online has become so widespread.. Search engines help us dig for information across the web. For example, Google’s search engine is intelligent enough to answer questions by extracting information from web pages. While search engines have their advantages, sometimes finding the information we want isn’t a straightforward process. Let’s look at the illustration below to understand how seeking information through search engines is different in comparison to people.

[Comparing information seeking through search engines vs. humans]

The illustration above depicts that information-seeking through other people can be more instructive, even if it comes at the cost of additional time. Seeking information through search engines can lead to dead ends because of content unavailability on a topic. Instead, we can ask questions of others.

## What is Quora?
Quora is a social question-and-answer service that allows users to ask questions to other users. Quora was created because of the issue that asking questions from search engines results in fast answers but shallow information. Instead, we can ask the general public, which feels more conversational and can result in deeper understanding, even if it’s slower. Quora enables anyone to ask questions, and anyone can reply. Furthermore, there are domain experts that have in-depth knowledge of a specific topic who occasionally share their expertise by answering questions.

The following plot shows global user search trends for the term “Quora” using Google:

[Popularity of Quora according to Google by year]

More than 300 million monthly active users post thousands of questions daily related to more than 400,000 topics on Quora.

In this chapter, we’ll design Quora and evaluate how it fulfills the functional and non-functional requirements.

## How will we design Quora?
We'll design Quora by dividing the design problem into the following four lessons.

1. Requirements: This lesson will focus on the functional and non-functional requirements for designing Quora. We’ll also estimate the resources required to design the system.
2. Initial design: We’ll create an initial design that fulfills all the functional requirements for Quora and also formulate the API design in this lesson. Primarily, we’ll discuss the system’s building blocks, other components involved in completing the design, their integration, and workflow.
3. Final design: In this lesson, we’ll start by identifying the limitations of the initial design. Then, we’ll update our final design to fulfill all the functional and non-functional requirements while addressing these limitations. We’ll also focus on some interesting aspects of our design, like vertical sharding of the database.
4. Evaluation: We’ll assess our design specifically for non-functional requirements and discuss some of its trade-offs. We’ll also discuss some ideas on how we can improve the availability of our design in this lesson.

```
Note: The information provided in this chapter is inspired by the engineering blog of Quora.
```
