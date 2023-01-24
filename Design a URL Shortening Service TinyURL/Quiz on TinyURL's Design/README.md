# Quiz on TinyURL's Design
```
1 In the URL shortener system’s design, the main reason to change the base of the sequencer to 58 was:

A)
To make the generated short URLs more secure.

B)
To enhance the readability of the generated short URLs.

C)
To improve the system’s availability.

D)
To ensure the system’s low latency.
```

```
2 In the system design phase, which reason below was the reason why we decided to use MongoDB?

A)
It has a higher write throughput as compared to reading.

B)
It ensures atomicity upon concurrent writes.

C)
It is the only NoSQL database for more specific problems like TinyURL.

D)
It’s easier to scale MongoDB as compared to other leader-less NoSQL databases.
```

```
3 (Select all that apply.) To meet the functional requirement of creating a custom alias for the short link, which of the following restriction(s) do we need to impose on the custom_alias variable for the API call?

You can select multiple correct answers.

A)
The length of the custom_alias shouldn’t be greater than the allowed character limit of the short links.

B)
The user must declare the value of the custom_alias variable.

C)
Every time a user creates a short link, a single user must enter the same custom_alias.

D)
The custom_alias should not contain the look-alike removed characters.
```

```
4 Which strategy did we adopt to counter the predictability of the sequencer-generated unique IDs?

A)
We changed the base of the sequencer to 58.

B)
We randomly selected a unique ID from the available pool for each short URL generation.

C)
We added a load balancer before the sequencer.

D)
We eliminated the alpha-numeric characters.
```

Answers

```
1
In the URL shortener system’s design, the main reason to change the base of the sequencer to 58 was:

A)
To make the generated short URLs more secure.

Explanation
Security is independent of the base of the sequencer.

Your Answer
B)
To enhance the readability of the generated short URLs.

Explanation
We change the base to 58 to remove the look-alike characters.

C)
To improve the system’s availability.

Explanation
Availability has no direct correspondence with the base of the sequencer.

D)
To ensure the system’s low latency.

Explanation
Low-latency has no direct correspondence with the base of the sequencer.
```

```
2
In the system design phase, which reason below was the reason why we decided to use MongoDB?

A)
It has a higher write throughput as compared to reading.

Explanation
The opposite is true for MongoDB.

Selected Option
B)
It ensures atomicity upon concurrent writes.

C)
It is the only NoSQL database for more specific problems like TinyURL.

Explanation
It is a very vague statement and, more importantly, false. Every database has its pros and cons.

D)
It’s easier to scale MongoDB as compared to other leader-less NoSQL databases.

Explanation
All NoSQL databases are easily scalable, and such a comparison is not readily available.
```

```
3
(Select all that apply.) To meet the functional requirement of creating a custom alias for the short link, which of the following restriction(s) do we need to impose on the custom_alias variable for the API call?

You can select multiple correct answers.

Selected Option
A)
The length of the custom_alias shouldn’t be greater than the allowed character limit of the short links.

Explanation
In our case, we have limited to 11 alpha-numeric characters from base-58.

B)
The user must declare the value of the custom_alias variable.

Explanation
It’s not a requirement of the system we designed, as the default value is None.

C)
Every time a user creates a short link, a single user must enter the same custom_alias.

Explanation
It’s a possibility but not a requirement; we can update the long URL against the custom URLs, but it’s not mandatory for a user.

Selected Option
D)
The custom_alias should not contain the look-alike removed characters.

Explanation
It’s an essential requirement to just include the allowed base-58 characters for custom_alias.
```

4. (B)
