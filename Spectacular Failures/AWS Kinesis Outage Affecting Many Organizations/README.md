# Quiz on the Sharded Counters' Design
```
1 What kind of problem would occur if our system created a counter with a few shards for a post from a user with one million followers?

A)
High read contention

B)
High write contention

C)
Users face delays on a read request

D)
Users get a quick response on the liked post
```

```
2 (Select all that apply.) What problem might arise if shards are selected in an order (sequentially) rather than randomly?

A)
The write request queue increases.

B)
Maximum shard utilization decreases.

C)
One-by-one selection of shards will take more time.

D)
The user will not get quick responses.
```

```
3 (Select all that apply.) Which situation needs a larger number of sharded counters to handle the traffic on YouTube?

A)
A video posted by a channel with millions of subscribers

B)
A video with a few likes over a long period of time

C)
A video with millions of views but a few dislikes

D)
Long videos posted by a channel with a few subscribers
```

Answers
1. (B) 
2. (A) (B) (D)
3. (A) (C)
