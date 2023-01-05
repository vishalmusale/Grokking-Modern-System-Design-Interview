# Quiz on the Distributed Messaging Queue’s Design
```
1. What kind of messages do dead-letter queues contain?

A)
The messages that have been consumed successfully.

B)
The messages that failed to be consumed and have reached the maximum attempts limit.

C)
The messages that have been produced by a process that’s dead now.

D)
None of the above
```

```
2. The purpose of replicating queues on multiple servers is to enhance the _________ of the system.

A)
security

B)
consistency

C)
availability

D)
None of the above
```

```
3. In the cluster of independent hosts model, which component is responsible for replicating messages in the other nodes?

A)
The front-end server

B)
The cluster manager

C)
Any random host within the cluster

D)
None of the above
```

```
4. The purpose of a metadata service is _________.

A)
to store messages in the queues along with their metadata

B)
to store, retrieve, and update the metadata of queues in the metadata store and cache

C)
to provide security features in accessing the queues

D)
None of the above
```

```
5. Which of the following is responsible for partitioning the queue and assigning a primary node to each partition?

A)
The internal cluster manager

B)
The external cluster manager

C)
The primary node

D)
One of the secondary nodes
```


# Answers on the Distributed Messaging Queue’s Design
```
1. What kind of messages do dead-letter queues contain? (B)

A)
The messages that have been consumed successfully.

B)
The messages that failed to be consumed and have reached the maximum attempts limit.

Explanation
A dead letter cannot be delivered or returned because it lacks appropriate directions. Similarly, a queue named after the dead-letter contains those messages that have failed to be consumed after the maximum attempts limit.

C)
The messages that have been produced by a process that’s dead now.

D)
None of the above
```

```
2. The purpose of replicating queues on multiple servers is to enhance the _________ of the system. (C)

A)
security

B)
consistency

C)
availability

Explanation
The purpose of replicating the queues and corresponding messages on multiple nodes is to increase the system’s availability. When one node is down, another stand-by server can serve the request.

D)
None of the above
```

```
3. In the cluster of independent hosts model, which component is responsible for replicating messages in the other nodes? (C)

A)
The front-end server

B)
The cluster manager

C)
Any random host within the cluster

Explanation
In the cluster of independent hosts model, a random host can receive the message responsible for replicating messages in other hosts in the respective queues.

D)
None of the above
```

```
4. The purpose of a metadata service is _________. (B)

A)
to store messages in the queues along with their metadata

B)
to store, retrieve, and update the metadata of queues in the metadata store and cache

Explanation
Metadata service acts as a middleware between the frontend and metadata storages (and caches). It is responsible for storing, retrieving, and updating the metadata of queues in the metadata stores and caches.

C)
to provide security features in accessing the queues

D)
None of the above
```

```
5. Which of the following is responsible for partitioning the queue and assigning a primary node to each partition? (A)

A)
The internal cluster manager

Explanation
The internal cluster manager partitions a queue into multiple parts and assigns a primary node to each partition. In contrast, the external cluster manager assigns clusters to each queue partition.

B)
The external cluster manager

C)
The primary node

D)
One of the secondary nodes
```
