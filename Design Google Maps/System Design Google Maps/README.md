# System Design: Google Maps
## What is Google Maps?
Let’s introduce the problem by assuming that we want to travel from one place to another. Here are the possible things that we might want to know:

- What are the best possible paths that take us to our destination, depending on the vehicle type we’re using?
- How long in miles is each path?
- How much time does each path take to get us to our destination?
A maps application (like Google Maps or Apple Maps) enables users to answer all of the above questions easily. The following illustration shows the paths calculated by Google maps from “Los Angeles, USA” to “New York City, USA.”

[Three paths suggested by Google maps for traveling from Los Angeles to New York](./map.jpg)

## When do we use a maps service?
Individuals and organizations rely on location data to navigate around the world. Maps help in these cases:

- Individuals can find the locations of and directions to new places quickly, instead of wasting their time and the costs of travel, such as gas.
- Individuals use maps to see their estimated time of arrival (ETA) and the shortest path based on current traffic data.
- Many modern applications rely heavily on maps, such as ride-hailing services, autonomous vehicles, and hiking maps. For example:
  - Waymo’s self-driving car system uses Google Maps to navigate efficiently, quickly, and safely.
  - Uber uses Google Maps as part of its application to assist drivers and provide customers with a visual representation of their journey.
- Routing and logistics-based companies reduce the time it takes to make deliveries. By using a map’s unique real-time and historical traffic data, it minimizes the overall cost of deliveries by reducing gas usage and time spent stuck in traffic.
In 2022, more than five million businesses are using Google Maps. It provides an API for enterprises to use a map system in their application.

## How will we design Google Maps?
We divide the design of Google Maps into five lessons:

1. Requirements: In this lesson, we’ll list the functional and non-functional requirements of a Google Maps system. We will also identify the challenges involved in designing such a system. Lastly, we’ll estimate the resources like servers and bandwidth needed to serve queries by millions of users.
2. Design: This lesson consists of the high-level and API design of a system like Google maps. We’ll describe the services and the workflow of the system.
3. Meeting the challenges: We will discuss how we overcome the challenges that we highlighted in the requirements lesson.
4. Detailed design: Based on the solution to the challenges, we will improve our earlier design and also elaborate on different aspects of it. We will describe the detailed design, including storage schema.
5. Evaluation: This lesson explains how our designed Google Maps system fulfills all the requirements.
Let’s start by understanding the requirements for designing a system like Google Maps.
