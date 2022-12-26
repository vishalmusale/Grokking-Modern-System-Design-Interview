# Availability

## What is availability?

### Measuring availability
Mathematically, availability, A, is a ratio. The higher the A value, the better. We can also write this up as a formula:

A (in percent) = (total time - amount of time service was down)/total time * 100

[the nines](./nine_availability.jpg)

We measure availability as a number of nines. The following table shows how much downtime is permitted when we’re using a given number of nines.

## Availability and service providers
Each service provider may start measuring availability at different points in time. Some cloud providers start measuring it when they first offer the service, while some measure it for specific clients when they start using the service. Some providers might not reduce their reported availability numbers if their service was not down for all the clients. The planned downtimes are excluded. Downtime due to cyberattacks might not be incorporated into the calculation of availability. Therefore, we should carefully understand how a specific provider calculates their availability numbers.


