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
#### Defination
Goal: Systematically search through a gragh
Algorithm (mimic maze exploration):
```java
DFS (to visit a vertex v){
    Mark v as visited;
    Recursively visit all unmarked verteces w adjacent to v.
}
```
#### Typical application
- Find all verteces connected to a given source vertex (connected group).
- Find a path between 2 verteces (I think using BFS is better).

#### Design pattern for Gragh processing
Decouple Gragh data type from gragh processing
- Create a Gragh object
- Pass the Gragh to a Gragh Processing routine. (Pass a Gragh and a source vertex)
- Query the Gragh Processing routing for information.
```java
public class Paths{
    Paths(Gragh G, int s)
    boolean hasPathTo(int v) //is there a path from s to v
    Iterable<Integer> pathTo(int v) // all the path from s to v; null if no such path
}
```

#### DFS
Goal
- find all the verteces connected to s (and a corresponding path)

Algorithm 
- Recursively visit all the verteces connected to one vertex;
- Mark each visited vertex;
- Return when no unvisited options

#### Implementation
```java
public class DeepFirstSearch{
    private boolean[] marked;
    private int[] edgeTo; // To keep the tree of paths
    private int s; // Source of the DFS
    
    public DeepFirstSearch(Gragh G, int s){
        this.marked = new boolean[G.V()];
        this.edgeTo = new boolean[G.V()];
        this.s = s;
        dfs(G, s);
    }
    
    private void dfs(G, v){
        marked[v] = true;
        for(int w : G.adj(v)){
            if(!marked[w]){
                dfs(G, w);
                edgeTo[w] = v;
            }
        }
    }
}
```
#### Analys
The time is proportional to the degree of source s.
## BFS
## CC
## Gragh Challenges
