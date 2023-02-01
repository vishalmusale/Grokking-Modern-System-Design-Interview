# Quiz on the Typeahead Suggestion System’s Design
```
1
Which component is responsible for updating the trie offline in the design of the typeahead suggestion system?

A)
The assembler

B)
The suggestion service

C)
ZooKeeper

D)
None of the above
```

```
2
What is the purpose of MapRreduce in the design of the typeahead suggestion system?

A)
To disseminate data toward a database for storage

B)
To aggregate the prefix count

C)
To increase the number of required operations for optimization

D)
None of the above
```

```
3
Why do we aggregate the counts and update them offline in their respective shards?

A)
To enhance the write operations

B)
To provide accurate results to the user

C)
To minimize the latency of the read operations

D)
None of the above
```

```
4
(Select all that apply.) Why is the trie partitioned and stored on several servers?

A)
To reduce the load on a single server

B)
To store more data

C)
To increase the performance of the system

D)
None of the above
```

```
5
(Select all that apply.) The replication of the trie partition is required to enhance ________.

A)
fault tolerance

B)
the durability of the data

C)
the security of the data
```

Answers
1. (A)
2. (B)
3. (C)
4. (A) (C)
5. (A) (B)
