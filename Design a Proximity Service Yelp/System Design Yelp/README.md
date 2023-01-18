# System Design: Yelp
## What is Yelp?
Yelp is a one-stop platform for consumers to discover, connect, and transact with local businesses. With it, users can join a waitlist, make a reservation, schedule an appointment, or purchase goods easily. Yelp also provides information, photos, and reviews about local businesses.

The user provides the name of a place or its GPS location, and the system finds places that are nearby. The user can also upload their opinions on this platform in the form of text, pictures, or ratings for a place they visited. Other location-based services include Foursquare and Google Nearby.

Services based on proximity servers are helpful in finding nearby attractions such as restaurants, theaters, or recreational sites. Designing such a system is challenging because we have to efficiently find all the possible places in a given radius with minimum latency. This means that we have to narrow down all the locations in the world, which could be in the billions, and only pinpoint the relevant ones.

[Yelp](./yelp)

## How will we design Yelp?
Here is the breakdown of Yelp’s design:

1。Requirements: In this lesson, we define the requirements and estimate the required servers, storage, and bandwidth of our system.
2。Design:In this lesson, we define the API design, the database schema, the components of our system, and the workflow of Yelp.
3。Design considerations: In this lesson, we dive deep into the design of the Yelp system.
4。Quiz: In this lesson, we take a quiz to test our knowledge of Yelp design.
Let’s start our design by defining its requirements.
