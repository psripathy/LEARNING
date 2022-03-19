[Data Structures - GeeksforGeeks](https://www.geeksforgeeks.org/data-structures/?ref=shm)

**Big O notations**

***Time Complexity***
```markdown
CONSTANT		  O(1)
LOGARITHMIC   O(log n)
LINEAR   		  O(n)
QUADRATIC   	O(n^2)
EXPONENTIAL   O(2^n)
```
![bigO](https://user-images.githubusercontent.com/34107462/155045179-3fb259ed-b302-4026-8902-5a2bc2d23dde.png)

***Space Complexity***


***Queue - FIFO***
Time Complexity - Enqueue, Dequeue, isEmpty, peek or front = O(1)
Space Complexity - O(n)

***Stack - LIFO***
Time Complexity - push, pop, peek = O(1)
Space Complexity - O(n)

***Breadth First Search - Queue is used to implement***
Used mostly in finding shortest path in unweighted graph. eg. Wall & Gates, No. of Islands, Open the lock etc.
Time Complexity - O(V+E) - V is vertices, E is edges
Space Complexity - O(V)

***Depth First Search - Recursion is used to implement*** (which translates to using Stack for method calls in the background)
Can also be used to find from root to target node. Can also be used to find connected components, determine connectivity, find bridges. eg. No of Islands, clone graph, target sum etc.
Time Complexity - O(V+E) - V is vertices, E is edges
Space Complexity - O(V)
