# Rate Limiter Algorithms
## Algorithms for rate limiting
The task of a rate limiter is directed by highly efficient algorithms, each of which has distinct advantages and disadvantages. However, there is always a choice to choose an algorithm or combination of algorithms depending on what we need at a given time. While different algorithms are used in addition to those below, we’ll take a look at the following popular algorithms.

- Token bucket
- Leaking bucket
- Fixed window counter
- Sliding window log
- Sliding window counter

### Token bucket algorithm
This algorithm uses the analogy of a bucket with a predefined capacity of tokens. The bucket is periodically filled with tokens at a constant rate. A token can be considered as a packet of some specific size. Hence, the algorithm checks for the token in the bucket each time we receive a request. There should be at least one token to process the request further.

The flow of the token bucket algorithm is as follows:

Assume that we have a predefined rate limit of R and the total capacity of the bucket is C
1. The algorithm adds a new token to the bucket after every 1/R seconds.
2. The algorithm discards the new incoming tokens when the number of tokens in the bucket is equal to the total capacity C of the bucket.
3. If there are N incoming requests and the bucket has at least N tokens, the tokens are consumed, and requests are forwarded for further processing.
4. If there are N incoming requests and the bucket has a lower number of tokens, then the number of requests accepted equals the number of available tokens in the bucket.
The following illustration represents the working of the token bucket algorithm.

[How the token bucket algorithm works]

The following illustration demonstrates how token consumption and rate-limiting logic work. In this example, the capacity of the bucket is three, and it is refilled at a rate of three tokens per minute.

[Token bucket]

#### Essential parameters
We require the following essential parameters to implement the token bucket algorithm:

- Bucket capacity(C): The maximum number of tokens that can reside in the bucket.
- Rate limit (R): The number of requests we want to limit per unit time.
- Refill rate (1/R): The number of tokens put into the bucket per unit time.
- Requests count (N): This parameter tracks the number of incoming requests and compares them with the bucket’s capacity.

#### Advantages
- This algorithm can cause a burst of traffic as long as there are enough tokens in the bucket.
- It is space efficient. The memory needed for the algorithm is nominal due to limited states.
#### Disadvantages
- From the implementation perspective, a lock might require taking a token from the bucket that can increase the request’s processing delay if contention on the lock increases.
- Choosing an optimal value for the essential parameters is a difficult task.

### The leaking bucket algorithm
The leaking bucket algorithm is a variant of the token bucket algorithm with slight modifications. Instead of using tokens, the leaking bucket algorithm uses a bucket to contain incoming requests and processes them at a constant outgoing rate. This algorithm uses the analogy of a water bucket leaking at a constant rate. Similarly, in this algorithm, the requests arrive at a variable rate. The algorithm process these requests at a constant rate in a first-in-first-out (FIFO) order.

Let’s look at how the leaking bucket algorithm works in the illustration below:

Essential parameters
Advantages
Disadvantages
### Fixed window counter algorithm
Essential parameters
Advantages
Disadvantages
### Sliding window log algorithm
Essential parameters
Advantages
Disadvantages
### Sliding window counter algorithm
Essential parameters
Advantages
Disadvantages
## A comparison of rate-limiting algorithms
## Conclusion
