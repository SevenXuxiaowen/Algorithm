
# Undirected Graph
## Gragh API
2 components of a Gragh object: `edges` and `vertices`
#### API Structure
```java
public class Gragh{
    Graph (int v) // Create a empty gragh with v vertices
    Gragh (In in) // Create a gragh with a set of input
    void addEdges(int v, int w) // Create an edge between 2 vertices v and w
    Iterable<Integer> adj(int v) // Vertices adjacent to v
    int V() // Count the number of vertices
    int E() // Count the number of edges
    String toString() // String representation
}
```
#### Typical gragh processing code
Compute the degree of v (the number of vertice that adjacent to v)
```java
public static int degree(Gragh G, int v){
    int degree = 0;
    for(int i : G.adj(v)) degree++;
    return degree;
}
```
Compute the maxmum of degree
```java
public static int maxDegree(Gragh G){
    int max = 0;
    for(int i = 0; i < G.V(); i++)
        if(degree(G, i) > max)
            max = degree(G, i);
    return max;
}
```
Compute average degree
```java
public static double averageDegree(Gragh G){
    return 2.0 * G.E() / G.V();
}
```
count self-loops
```java
public static int numberOfSelfLoops(Gragh G){
    int count = 0;
    for(int i = 0; i < G.V(); i++){
        for(int j : G.adj(i)){
            if(i == j) count++;
        }
    }
    return count/2;
}
```
#### Implementation
- 1/List of edges;
- 2/Maintain 2-dimensional v-by-v boolean array, if v connects to w, adj[v][w] = adj[w][v] = true;
- 3/Maintain vertex-indexe array of list (Using this method to implement)
```java
public class Gragh{
    private final int V;
    private Bag<Integer>[] adj;
    public Gragh(int V){
        this.V = V;
        adj = (Bag<Integer>[]) new Bag[V];
        for(int v = 0; v < V; v++){
            adj[v] = new Bag<Integer>;
        }
    }
    public void addEdges(int v, int w){
        adj[v].add(w);
        adj[w].add(v);
    }
    
    public Interable<Integer> adj(int v){
        return adj[v];
    }
}
```
#### Analyzing the 3 implementation
List of edjes
- space : `E`
- addEdges : `1`
- v and w connected? : `E`
- iterate the adj(v) : `E`

Adjaceny matrix
- space: `V^2`
- addEdges : `1`
- v and w connected? : `1`
- iterate the adj(v) : `V`

Adjacenty lists
- space: `E + V`
- addEdges : `1`
- v and w connected? : `degree(v)`
- iterate the adj(v) : `degree(v)`
## DFS
## BFS
## CC
## Gragh Challenges
