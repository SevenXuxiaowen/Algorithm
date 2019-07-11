# Balanced BST
## Elementary symbol table
#### Sequential search (unordered linkedlist)
1. Data Structure: maintain an unordered linked list of key-value pair
2. Search: Scan through all keys until find a match
3. Insert: Scan through all keys until find a match, if no match add to the front
- Worst-case-cost (after N insert): search - ```N```, insert - ```N```, delete - ```N```
- Average-case (after N insert): search hit - ```N/2```, insert - ```N/2```, delete - ```N/2```
- Ordered iteration: NO
- Key iterface: equals()
#### Binary search (ordered array)
1. Data Structure: maintain an ordered array of key-value pair
2. Helper rank function: find the rank number of the array (so you can return the element by querry ```array[rank(key)]```)
- Worst-case-cost (after N insert): search - ```lgN```, insert - ```N```, delete - ```N``` 
- Average-case (after N insert): search - ```lgN```, insert - ```N/2```, delete - ```N/2```
- Ordered iteration: YES
- Key interface: ```compareTo()```
#### BST
1. Symmetric order: each node has a key, left branch is smaller, right branch is bigger. In other words, inorder traversal yeilds keys in an ascending order.
2. Search: if less, go left; if greater, go right; recursion. If equal, search hit.
3. Insert: if less, go left; if greater, go right; recursion. if null, insert.
- Worst-case-cost (after N insert): search - ```N```, insert - ```N```, delete - ```N```
- Average-case (after N insert): search - ```1.39lgN```, insert - ```1.39lgN```
- Odered iteration: YES
- Key interface: ```compareTo()```
## 2-3 Tree
Guaranteed logarithmic performance for search and insert.
1. Symmetric order: Inorder traversal yeilds keys in ascending order.
2. Perfect balance: Every path from root to null link has the same length.
#### Search
Same as BST, if meet 3 node, less go left, greater go right, interval go middle
#### Insert
- Add new key to 3 node to create temporary 4-node
- Move middle key in 4-node to parent
- Repeat up the tree as neccesary
- If you reach a node that is 4-node, split it up to three 2-nodes
#### Tree hight (c)
- Worst case: ```lgN``` (all 2-nodes)
- Best case: ```log3N``` = ```0.631lgN1``` (all 3-nodes)
#### Comlicity
- Worst-case-cost: search - ```clgN```, insert - ```clgN```, delete - ```clgN```
- Average-case-cost: search - ```clgN```, insert - ```clgN```, delete - ```clgN```
- Odered iteration: YES
- Key interface: ```compareTo()```
## Red-black BSTs
#### Defination: Left Leaning Red-black BSTs
Represent 2-3 trees as BST by using 'internal' left-leaning links as 'glue' for 3 nodes.
- No node has 2 red links connected to it.
- Every path from root to null has the same number of black links.
- Red links lean left.
#### Construction
Compared with BST node, the left leaning red-black BSTs node has one boolean color feilds, refering to the color of its parent link.
```java
publich class LLRB{
    private static final boolean RED = true;
    private static final boolean BLACK = false;
    private class Node{
        Key key;
        Value val;
        Node left, right;
        boolean color;
    }
    private boolean isRed(Node x){
        if(x == null) return false; //null links are BLACK
        return x.color == RED;
    }
}
```
#### Left rotation
```java
private Node rotateLeft(Node h){
    Node x = h.right;
    h.right = x.left;
    x.left = h;
    x.color = h.color;
    h.color = RED;
    return x;
}
```
#### Right rotation
```java
private Node rotateRight(Node h){
    Node x = h.left;
    h.left = x.right;
    x.right = h;
    x.color = h.color;
    h.color = RED;
    return x;
}
```
#### Color flip
```java
private void flipColors{
    h.color = RED;
    h.left.color = BLACK;
    h.right.color = BLACK;
}
```





