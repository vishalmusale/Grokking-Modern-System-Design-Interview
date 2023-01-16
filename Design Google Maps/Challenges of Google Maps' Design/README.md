# Challenges of Google Maps' Design

## Meeting the challenges
We listed two challenges in the Introduction lesson: scalability and ETA computation. Let’s see how we meet these challenges.

### Scalability
Scalability is about the ability to efficiently process a huge road network graph. We have a graph with billions of vertices and edges, and the key challenges are inefficient loading, updating, and performing computations. For example, we have to traverse the whole graph to find the shortest path. This results in increased query time for the user. So, what could be the solution to this problem?

The idea is to break down a large graph into smaller subgraphs, or partitions. The subgraphs can be processed and queried in parallel. As a result, the graph construction and query processing time will be greatly decreased. So, we divide the globe into small parts called segments. Each segment corresponds to a subgraph.

#### Segment
A segment is a small area on which we can work easily. Finding paths within these segments works because the segment’s road network graph is small and can be loaded easily in the main memory, updated, and traversed. A city, for example, can be divided into hundreds of segments, each measuring 5×5 miles.

```
Traversing is visiting the graph vertices to reach a specific vertex.
```

```
Note: A segment is not necessarily a square. It can also be a polygon. However, we are assuming square segments for ease of explanation.
```
Each segment has four coordinates that help determine which segment the user is in. Each coordinate consists of two values, the latitude and longitude.

[Partitioning the globe into small segments, and each segment has four coordinates with latitude and longitude values]

Let’s talk about finding paths between two locations within a segment. We have a graph representing the road network in that segment. Each intersection/junction acts as a vertex and each road acts as an edge. The graph is weighted, and there could be multiple weights on each edge—such as distance, time, and traffic—to find the optimal path. For a given source and destination, there can be multiple paths. We can use any of the graph algorithms on that segment’s graph to find the shortest paths. The most common shortest path algorithm is the Dijkstra’s algorithm.

```
The traditional Dijkstra algorithm performs a guided search to find the shortest path. However, it comes at the cost of an increased query time. We have to set a limit on the query time because we wouldn’t want the user to wait too long to get their results. So, we’ll go with finding the optimal path within the given time cost.

The A* algorithm is an extension of the Dijkstra algorithm that uses heuristics to guide its search. Instead of finding the shortest path, A* finds the optimal path that is calculated by minimizing the following function.

f(n)=g(n)+h(n)

Here, n is the next node on the path, g(n) is the cost of the path from the start node to n, and h(n) is a heuristic function that estimates the cost of the cheapest path from n to the goal.
```

```
Note: There are some algorithms that are specifically designed for road networks that focus on achieving shorter query time. These algorithms are A*, Arc flags, contraction hierarchies, transit node routing, reach-based routing, and hub labeling.
https://arxiv.org/pdf/1603.01607.pdf
http://www.diag.uniroma1.it/challenge9/papers/kohler.pdf
https://en.wikipedia.org/wiki/Contraction_hierarchies
https://www.researchgate.net/publication/6366597_Fast_Routing_in_Road_Networks_with_Transit_Nodes
https://archive.siam.org/meetings/alenex04/abstacts/rgutman1.pdf
https://www.microsoft.com/en-us/research/wp-content/uploads/2010/12/HL-TR.pdf
```

After running the shortest path algorithm on the segment’s graph, we store the algorithm’s output in a distributed storage to avoid recalculation and cache the most requested routes. The algorithm’s output is the shortest distance in meters or miles between every two vertices in the graph, the time it takes to travel via the shortest path, and the list of vertices along every shortest path. All of the above processing (running the shortest path algorithm on the segment graph) is done offline (not on a user’s critical path).

[Finding a path between vertices within a segment]

The illustration above shows how we can find the shortest distance in terms of miles between two points. For example, the minimum distance (m) between points A and D is 11 miles by taking the path A->C->D. It has an ETA of 15 minutes.

We’ve found the shortest path between two vertices. What if we have to find the path between two points that lie on the edges? What we do is find the vertices of the edge on which the points lie, calculate the distance of the point from the identified vertices, and choose the vertices that make the shorter total distance between the source and the destination. The distance from the source (and destination) to the nearest vertices is approximated using latitude/longitude values.

[Choosing a path between points that lie on the edge]

We’re able to find the shortest paths within the segment. Let’s see what happens when the source and the destination belong to two different segments, and how we connect the segments.

#### Connect two segments
### ETA computation
