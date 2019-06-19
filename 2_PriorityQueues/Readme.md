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

| Implementation | Times   | Space |
|:---------------|:-------:|:-----:|
|Sort            | NlgN    | NlgN  |
|elementry PQ    | MN      | M     | 
|binary heap     | NlogM   | M     | 

## Elementry PQ
UnorderedMaxPQ implementation
```java
public class UnorderedMaxPQ<Key extends Comparable<Key>>{
    private Key[] pq;
    private int N;
    
    public UnorderedMaxPQ(int capacity){
        pq = (Key[]) Comparable[Capacity]; //Note: no generic array creation
    }
    
    public void insert(Key v){ pq[N++] = v; }
    
    public Key delMax(){
        int max = 0;
        for(int i = 0; i < N; i++){
            if (less(pq[max], pq[i]) max = i;
        }
        exch(max, N - 1);
        return pq[--N];
    }
    
    public boolean isEmpty(){ return N == 0; }
    
    public int size(){ return this.N; }
}
```
## Binary Heaps
#### Definition
Array representation of a heap ordered complete binary tree.
1. Heap ordered: Parent nodes no smaller than child nodes.
2. Array representation: in place, indices start at 1.(so first node of every level always start at 1, 2, 4, ... , 2^n)
3. Proposition: Parent of node [k] is [k/2]. Children of node [k] is [2*k] and [2*k+1].
#### Some helper functions
1. Swim(): Child's key become larger key than its parent's key --> exchange child's key with parent's repeately utill it's right.
```java
private void swim(int k){
    while(k > 1 && less(k, k/2){
        exch(k, k/2);
        k = k / 2;
    }
}
```
2. Sink(): Parent's key become smaller than one (or both) of its childen's key --> exchange parent's key with larger one of its children's key repeatedly utill it's right.
```java
private void sink(int k){
    while(2k < N){
        int j = 2k;
        if (j < N && less(j, j + 1)) j++; //make j is the larger one of its children's key
        if(!less(k, j)) break;
        exch(k, j);
        k = j;
    }
}
```
3. Insertion in a heap: add one node at the end, swip it up.
```java
public void insert(Key x){
    pq[++N] = x;
    swim(N);
}
```
4. Delete the max node: exchange last node with the root node, sink it down, delete the last node
```java
public Key delMax(){
    Key max = pq[1];
    exch(1, N--);
    sink(1);
    pq[N+1] = null; // prevent loitering;
    return max;
}
```
## Heap Sort
#### Method
1. Heap Construction: Build a max binary heap using a bottom-up method.(也就是说从k=N/2开始一个一个往上遍历直到k=1)
```java
for(int k = N/2; k >= 1; k--){
    sink(a, k, N);
}
```
2. Sortdown: Repeatedly delete the largest remaining item.
- Remove the maximum, one at a time.(including change the root with tail, sink the exchanged root)
- Leave in array, instead of nulling out.
```java
while(N > 1){
    exch(a, 1, N--);
    sink(a, 1, N);
}
```
#### Heap Sort (Java implementation)
```java
public class Heap{
    public static void sort(Comparable[] a){
        int N = a.length;
        //Step 1: Heap construction
        for(int k = N / 2; k >= 1; k--){
            sink(a, k, N);
        }
        //Step 2: Sort down
        while(N > 1){
            exch(a, 1, N--);
            sink(a, 1, N);
        }
    }
    
    private static void sink(Comparable[] a, int k, int N){
        while( 2 * k < N){
            int j = 2 * k;
            if(j < N && less(j, j + 1)) j++;
            if(less(a, j, k) break;
            exch(a, k, j);
            k = j;
        }
    }
    
    private static void less(Comparable[] a, int i, int j){
        return a[i].compareTo(a[j]) < 0;
    }
    
    private static void exch(Comparable[] a, int i, int j){
        Comparable temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
}
```
#### Comparation of different sorting methods
1. Selection Sort - O(N^2)
2. Insertion Sort - O(N^2)
3. Quick Sort - O(NlnN)
4. 3-way Quick Sort - O(NlnN)
5. Merge Sort - O(NlgN) - stable and NlgN gurantee
6. Heap Sort - O(NlgN) - inplace and NlgN gurantee












