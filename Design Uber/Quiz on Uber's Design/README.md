# Quiz on Uber's Design
```
1 (Select all that apply.) Which factors can help optimize the ETA at the start of the trip to lower the cost and duration of the trip?

A)
Real-time traffic detail

B)
Distance of a driver before the trip starts

C)
Professional driver

D)
Speed of vehicle
```

```
2 (Select all that apply.) Why is it essential to store the information of routes in a ride-hailing service design?

A)
It helps to optimize the ETA.

B)
It minimizes the ride cost fluctuation.

C)
It helps to determine the bonus for the driver.

D)
It helps to engage more passengers.
```

```
3 (Select all that apply.) What information can we store in the CDN?

A)
Drivers’ current locations

B)
Driver and passenger profile details

C)
Last trips of the passengers

D)
The traffic details
```

Answers

1. (A) (D)

```
2
(Select all that apply.) Why is it essential to store the information of routes in a ride-hailing service design?

Selected
A)
It helps to optimize the ETA.

Explanation
We have actual values with each route stored in the database. Next time someone chooses this route, we could give a more accurate ETA.

Selected
B)
It minimizes the ride cost fluctuation.

Explanation
We know the route detail by the ride details. So, the ETA estimation will be close to the actual time taken. That’s why the initial cost estimate (decided earlier the ride) fluctuates less.

C)
It helps to determine the bonus for the driver.

Explanation
Saving the route detail does not affect the bonus. In contrast, the distance covered by the driver matters in bonus determination.

D)
It helps to engage more passengers.
```

```
3
(Select all that apply.) What information can we store in the CDN?

A)
Drivers’ current locations

Explanation
It will frequently change, so it is not suitable.

Selected
B)
Driver and passenger profile details

Explanation
Names, driver photos, vehicle detail, etc., can store in the CDN.

Selected
C)
Last trips of the passengers

Explanation
The trips detail of the passengers can be stored in the CDN because once a trip is over, these details don’t change.

D)
The traffic details

Explanation
Traffic is not consistent. It changes every second. CDN usually stores the static data that is not changed frequently.
```
