# Encoder for TinyURL

## Introduction
We've discussed the overall design of a short URL generator (SUG) in detail, but two aspects need more clarification:

1. How does encoding improve the readability of the short URL?
2. How are the sequencer and the base-58 encoder in the short URL generation related?

### Why to use encoding
Our sequencer generates a 64-bit ID in base-10, which can be converted to a base-64 short URL. Base-64 is the most common encoding for alphanumeric strings' generation. However, there are some inherent issues with sticking to the base-64 for this design problem: the generated short URL might have readability issues because of look-alike characters. Characters like O (capital o) and 0 (zero), I (capital I), and l (lower case L) can be confused while characters like + and / should be avoided because of other system-dependent encodings.

So, we slash out the six characters and use base-58 instead of base-64 (includes A-Z, a-z, 0-9, + and /) for enhanced readability purposes. Let's look at our base-58 definition.

```
Base-58
Value      Character     Value     Character    Value   Character    Value    Character

0            1            15          G          30       X           45          n

1            2            16          H          31       Y           46          o

2            3            17          J          32       Z           47          p

3            4            18          K          33       a           48          q

4            5            19          L          34       b           49          r

5            6            20          M          35       c           50          s

6            7            21          N          36       d           51          t

7            8            22          P          37       e           52          u

8            9            23          Q          38       f           53          v

9            A            24          R          39       g           54          w

10           B            25          S          40       h           55          x

11           C            26          T          41       i           56          y

12           D            27          U          42       j           57          z

13           E            28          V          43       k

14           F            29          W          44       m
```

```
The highlighted cells contain the succeeding characters of the omitted ones: 0, O, I, and l.
```

## Converting base-10 to base-58
Since we're converting base-10 numeric IDs to base-58 alphanumeric IDs, explaining the conversion process will be helpful in grasping the underlying mechanism as well as the overall scope of the SUG. To achieve the above functionality, we use the modulus function.

Process: We keep diving the base-10 number by 58, making note of the remainder at each step. We stop where there is no remainder left. Then we assign the character indexes to the remainders, starting from assigning the recent-most remainder to the left-most place and the oldest remainder to the right-most place.

Example: Let's assume that the selected unique ID is 2468135791013. The following steps show us the remainder calculations:

Base-10 = 2468135791013

2468135791013 % 58=17

42554065362 % 58=6

733690782 % 58=4

12649841 % 58=41

218100 % 58=20

3760 % 58=48

64 % 58=6

1 % 58=1
Now, we need to write the remainders in order of the most recent to the oldest order.

Base-58 = [1] [6] [48] [20] [41] [4] [6] [17]

Using the table above, we can write the associated characters with the remainders written above.

Base-58 = 27qMi57J

Note: Both the base-10 numeric IDs and base-64 alphanumeric IDs have 64-bits, as per our sequencer design.

Let's see the example above with the help of the following illustration.

[How a base-10 number is converted into a base-58 alphanumeric short URL]

## Converting base-58 to base-10
The decoding process holds equal importance as the encoding process, as we used a decoder in case of custom short URLs generation, as explained in the design lesson.

Process: The process of converting a base-58 number into a base-10 number is also straightforward. We just need to multiply each character index (value column from the table above) by the number of 58s that position holds, and add all the individual multiplication results.

Example: Let's reverse engineer the example above to see how decoding works.

Base-58: 27qMi57J

  2_{58} = 1 x 58^{7} = 2207984167552

  7_{58} = 6 x 58^{6} = 228412155264

  q_{58} = 48 x 58^{5} = 31505124864

  M_{58} = 20 x 58^{4} = 226329920

  i_{58} = 41 \times 58^{3} = 7999592

  5_{58} = 4 \times 58^{2} = 13456

  7_{58} = 6 \times 58^{1} = 348

  J_{58} = 17 \times 58^{0} = 17


Base-10 = 17 + 348 + 13456 + 7999592 + 226329920 + 31505124864 + 228412155264 + 2207984167552

Base-10 = 2468135791013.

This is the same unique ID of base-10 from the previous example.

Let's see the example above with the help of the following illustration.

[How a base-58 number is converted into a base-10 numeric ID]

## The scope of the short URL generator
The short URL generator is the backbone of our URL shortening service. The output of this short URL generator depends on the design-imposed limitations, as given below:

- The generated short URL should contain alphanumeric characters.
- None of the characters should look alike.
- The minimum default length of the generated short URL should be six characters.
These limitations define the scope of our short URL generator. We can define the scope, as shown below:

- Starting range: Our sequencer can generate a 64-bit binary number that ranges from 1 to (2^{64}-1). To meet the requirement for the minimum length of a short URL, we can select the sequencer IDs to start from at least 10 digits, i.e., 1 Billion.
- Ending point: The maximum number of digits in sequencer IDs that map into the short URL generator's output depends on the maximum utilization of 64 bits, that is, the largest base-10 number in 64-bits. We can estimate the total number of digits in any base by calculating these two points:
1. The numbers of bits to represent one digit in a base-n. This is given by log_2{n}
2. Number of digits = Total bits available/Number of bits to represent one digit

Let's see the calculations above for both the base-10 and base-58 mathematically:

  - Base-10:
    - The number of bits needed to represent one decimal digit = log_2{10} = 3.13
  - The total number of decimal digits in 64-bit numeric ID = 64 / 3.13= 20

Base-58:
The number of bits needed to represent one decimal digit = log_2{58}=5.85
The total number of base-58 digits in a 64-bit numeric ID =64 / 5.85=11

```
Maximum digits: The calculations above show that the maximum digits in the sequencer generated ID will be 20 and consequently, the maximum number of characters in the encoded short URL will be 11.  
```

```
Question 1
Since we’re using the 10 digits and beyond sequencer IDs, is there a way we can use the sequencer IDs shorter than 10 digits?

Answer
We can use the range below the ten digits sequencer IDs for custom short links for users with premium memberships. It will ensure two benefits:

Utilization of the blocked range of IDs
Less than six characters short URLs
Example: Let’s assume that the user requests abc as a custom short URL, and it’s available in our system, as there is no instance in the data store matching with this short URL. We need to perform the following two operations:

1. Assign this short URL to the requested long URL and store this record in the datastore.
2. Mark the associated unique ID unusable. To find the associated unique ID, we need to decode abc into base-10. Using the above decode method, we come up with the base-10 unique ID value as 113019. The unique ID is less than 1 Billion, as the custom short URL is less than six characters, conforming to the above-stated two benefits.
Our system doesn’t ensure a guaranteed custom short link generation, as some other premium member might have claimed the requested custom short URL.
```

```
Question 2
What should the short URL be for the sequencer’s largest number?

Hide Answer
Since the sequencer’s largest number is 18,446,744,073,709,551,615. That is, 2^{64}-1, the base-58 equivalent of it will be jpXCZedGfVQ, conforming to our calculations above.
```

## The sequencer's lifetime
The number of years that our sequencer can provide us with unique IDs depends on two factors:

- Total numbers available in the sequencer = 2^{64} - 10^{9} (starting from 1 Billion as discussed above)
- Number of requests per year = 200 Million per month×12=2.4 Billion (as assumed in Requirements)
So, taking the above two factors into consideration, we can calculate the expected life of our sequencer.

The lifetime of the sequencer = total numbers available/yearly requests ={2^{64}-10^{9}} / {2.4 Billion} = 7,686,143,363.63 years

```
            Life expectancy for sequencer
Number of requests per month	200 Million
Number of requests per year	  2.4 Billion
Lifetime of sequencer	        7,686,143,363.63 years
```
Therefore, our service can run for a long time before the range depletes.



