# Quiz on Yelp's Design
```
1　(Select all that apply.) Which requirement will not be fulfilled if we don’t constrain the number of segments to reduce the graph size?

A)
Availability

B)
Consistency

C)
Scalability

D)
Reliability
```

```
2 (True or False) The type of partitioning (region- or PlaceID-based) affects the structure of QuadTrees.

A)
True

B)
False
```

```
3 In which scenario is there a greater chance of delay in response time if we use the leader-follower approach to help us in replication?

A)
When the leader updates the followers asynchronously

B)
When the leader updates the followers synchronously

C)
When the leader saves the updates of a day and sends the changes to followers once a day
```

```
4 (Select all that apply.) What will happen if the leader and followers both die simultaneously?

A)
We would have to rebuild the QuadTrees.

B)
The performance will be affected.

C)
The availability will be affected.
```


Answers

```
1 (Select all that apply.) Which requirement will not be fulfilled if we don’t constrain the number of segments to reduce the graph size?

Selected Option
A)
Availability

Explanation
The query will return the results slower affecting the user response time.

B)
Consistency

Selected Option
C)
Scalability

Explanation
It won’t be easy to modify a humongous graph.

D)
Reliability
```

```
2 (True or False) The type of partitioning (region- or PlaceID-based) affects the structure of QuadTrees.

Correct Answer
A)
True

Explanation
Yes, it does as we have no assurance that each segment will have the same number of places in it. Though this won’t be an issue as we will be finding our neighboring segments within the defined radius.

B)
False
```

```
3 In which scenario is there a greater chance of delay in response time if we use the leader-follower approach to help us in replication?

A)
When the leader updates the followers asynchronously

Explanation
The leader will not wait until all followers have updated the data, it’ll update the data in its storage and then send the update to followers.

Correct Answer
B)
When the leader updates the followers synchronously

Explanation
The leader waits until all followers have updated the data.

C)
When the leader saves the updates of a day and sends the changes to followers once a day

Explanation
The leader will not ask the followers to update the data at once so there won’t be a delay.
```

```
4
(Select all that apply.) What will happen if the leader and followers both die simultaneously?

Selected Option
A)
We would have to rebuild the QuadTrees.

Explanation
We would have to rebuild QuadTrees from the key-value stores where we kept them.

Selected Option
B)
The performance will be affected.

Explanation
We would not be able to serve any user query which will affect the performance.

Selected Option
C)
The availability will be affected.

Explanation
Both leader and followers will be down so they will be unable to process the requests.
```
