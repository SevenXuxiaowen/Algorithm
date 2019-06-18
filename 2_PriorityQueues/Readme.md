# Priority Queues
## PQ API
#### API Requirement
key must be comparable
```java
public class MaxPQ<key extends Comparable<key>>{
            MaxPQ();          // Create an instance from empty
            MaxPQ(Key[] a);   // Create an instance from given keys 
       void insert(Key v);    // Insert a key into the priority queue
        Key delMax();         // Delete and return max element of the priority queue
    boolean isEmpty();        
        Key max();
        int size();
}
```
#### Application 
Find the largest M items in a stream of N items.
| Implementation | Times | Space |
|:---------------|:-----:|:-----:|
|Sort            | NlgN  |NlgN   |
|elementry PQ    | MN    |M      |
|binary heap     | NlogM |M      |
