# System Design: Google Docs
## Problem statement
Imagine two students are preparing a report on a project they’ve just completed. Since the students live apart, the first student asks the second student to start writing the report, and the first student will improve the received copy. Although quite motivated, the students soon understand that such a collaboration is disorganized. The following illustration shows how tedious the process can get.

[Problems arising when there’s no collaborative document editing service](./demo.jpg)

The scenario above is one example that leads to time wastage and frustration when users collaborate on a document by exchanging files with each other.

## Google Docs
To combat the problem above, we can use an online collaborative document editing service like Google Docs. Some advantages of using an online document editing service instead of a desktop application are as follows:

- Users can review and comment on a document while it’s being edited.
- There are no special hardware specifications required to get the latest features. A machine that can run a browser will suffice.
- It's possible to work from any location.
- Unlike local desktop editors, users can view long-term document history and restore an older version if need be.
- The service is free of cost.
Other than Google docs, some popular online editing services include Etherpad, Microsoft Office 365, Slite, and many others.


### Designing Google Docs
A collaborative document editing service can be designed in two ways:

- It could be designed as a centralized facility using client-server architecture to provide document editing service to all users.
- It could be designed using peer-to-peer technology to collaborate on a single document.


Most commercial solutions focus on client-service architecture to have finer control. Therefore, we’ll focus on designing a service using the client service architecture. Let’s see how we will progress in this chapter.

```
Note: According to a survey, 64% of people use Google Docs for document editing at least once a week.
See: https://www.statista.com/forecasts/1011649/frequency-of-using-google-docs-in-the-us

```

## How will we design Google Docs?
We've divided the design problem into four stages:

1. Requirements for Google Docs’ Design: This lesson will focus on establishing the requirements for designing a collaborative document editing service. We’ll also quantify the infrastructure requirements in this stage.
2. Google Docs’ Design: The goal of this lesson is to come up with a design that fulfills the requirements of the service. This lesson will explain why a component is used and how it integrates with other components to fulfill functional requirements.
3. Concurrency in Collaborative Editing: Online document editing services have to resolve conflicts between users editing the same portion of a document. This lesson covers the type of problems that can arise and the techniques used to resolve such conflicts.
4. Evaluating Google Docs’ Design: The main objective of this lesson is to evaluate our design for non-functional requirements. Mainly, we see if our design is performant, consistent, available, and scalable.
