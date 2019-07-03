# Symbol Table
## ST API
Associated Array Abstraction - Associated one value with a key.
```java
public class ST<Key, Value>{
                  ST() 
             void put(Key key, Value value)
            Value get(Key key)
             void delete(Key key)
          boolean contains(Key key)
          boolean isEmpty()
              int size()
    Iterable<Key> keys()
}
```
#### Implement equals() for 2 key
1. Optimization for reference equality;
2. Check against null
3. Check that 2 objects are the same type and cast
4. Compare each significant feild.
```java
public final class UserDefined implement Comparable<UserDefined> {
    // ... constructure and others
    // ...
    // ...
    
    public boolean equals(Objerct that){ // ====> parse type must be Object
        // 1. Check if the 2 are the same instance
        if (that == this) return true;
        // 2. Check if the 2 are the same class
        if (that.getClass() != that.getClass()) return false;
        // 3. Check if the object is null
        if (that == null) return false;
        // 4. Check if the value is same
        UserDefined y = (UserDefined) that;
        ...
        return true
    }
}
```
## Elementary implementations 
1. Sequential search in a linked list
Search - O(N), Insert - O(N), not ordered iteration.
2. Binary search in an ordered array
Search - O(lnN), Insert - O(N), ordered iteration.
```java
public Value get(Key key){
    if(isEmpty) return null;
    int i = rank(key);
    if(i < N && keys[i].compareTo(key) == 0) return vals[i];
    else return null;
}

private int rank(Key key){
    int lo = 0, hi = N-1;
    while(lo < hi){
        int mid = lo + (hi - lo) / 2;
        int cmp = key.compareTo(keys[mid]);
        if      (cmp > 0)  lo = mid + 1;
        else if (cmp < 0)  hi = mid - 1;
        else    (cmp == 0) return mid;
    }
    return null;
}
```
#### Comparation
| Implementations   | search | insert/delete | min/max | floor/ceiling | rank   | select | ordered iteration |
| ----------------- |:------:| :------------:|:-------:|:-------------:|:------:|:------:|:-----------------:|
| Sequential search |N       | N             |N        |N              |N       |N       |NlgN               |
| Binary search     |lgN     | N             |1        |lgN            |lgN     |1       |N                  |
| BST               |1.39lgN |1.39lgN        |1.39lgN  |1.39lgN        |1.39lgN |1.39lgN |N                  |

## BST
#### Definition: A BST is a binary search tree in symmetric order
- symmetric order: the key of the node is larger than all keys in its left subtree, smaller than all keys in the right subtree.
#### Node format
```java
private class Node{
	private Key key;
	private Value value;
	private Node left, right;
	private int count;
	
	public Node(Key key, Value value){
		this.key = key;
		this.value = value;
	}
}
```
#### Implementation
1.Basic class structure
```java
public class BST<Key extends Comparable<Key>, Valye>{
	private Node root; //In java, a BST is a reference to a root Node.
	private class Node{ /* see above */}
	public void put(Key key, Value value){ /* see below */ }
	public Value get(Key key){ /* see below */ }
	public void delete(Key key){ /* see below */ }
	public Iterable<Key> iterator(){ /* see below */ }
}
```
2. Get (Binary search)
```java
public Value get(Key key){
	Node cur = root;
	while(cur != null){
		int cmp = key.compareTo(cur.key);
		if(cmp > 0) cur = cur.right;
		else if(cmp < 0) cur = cur.left;
		else return cur.val;
	}
	return null;
}
```
3. Put (if larger, put in right, if smaller, put in left, recursively)
Number of compares = 1 + depth of node
```java
public void put(Key key, Value val){
	root = put(root, key, val);
}
private Node put(Node x, Key key, Value val){
	if(x == null) return new Node(key, val);
	int cmp = key.compareTo(x.key);
	if(cmp > 0) x.right = put(x.right, key, val);
	else if(cmp < 0) x.left = put(x.left, key, val);
	else x.value = val;
	
	x.count = 1 + size(x.left) + size(x.right);
	
	return x;
}
```
4. Floor
- Case 1: k equals the key at the root, the floor of k is k
- Case 2: k is less than the key at root, the floor of k is at the left subtree
- Case 3: k is larger than tha key at root: a) the root is floor if all the nodes at its right subtree is larger than k (return null); b) there is other floor, the floor of k is at the right subtree.
```java
public Key floor(Key key){
	Node x = floor(root, key);
	if(x == null) return null;
	return x.key;
}
public Key floor(Node x, Key key){
	if(x == null) return null;
	int cmp = key.compareTo(x.key);
	
	if(cmp = 0) return x;
	if(cmp < 0) return floor(x.left, key);
	
	Node t = floor(x.right, key);
	if(t != null) return t;
	else return x
}
```
5. Subtree counts
```java
public int size(){ return size(root) }
private int size(Node x){ 
	if (x == null) return 0;
	return x.count;
}
```
6. Rank
```java
public int rank(Key key){ return rank(key, root); }
private int rank(Key key, Node x){
	if(x == null) return 0;
	int cmp = key.compareTo(x.key);
	if(cmp < 0) return rank(key, x.left);
	if(cmp > 0) return 1 + size(x.left) + rank(key, x.right);
	else return size(x.left);
}
```
7. Inorder traversal
```java
public Iterable<Key> keys(){
	Queue<Key> q = new Queue<Key>();
	inorder(root, q);
	return q;
}
private void inorder(Node x, Quere<Key> q){
	if(x == null) return;
	inorder(x.left, q);
	q.enqueue(x.key);
	inorder(x.right, q);
}
```
## BST Deletion
#### Deleting the minimum
1. Go left untill find a node witl null left link
2. Replace the node with its right link
3. Update subtree count
```java
private void deleteMin(){
	root = deleteMin(root);
}
private Node deleteMin(Node x){
	if(x.left == null) return x.right;
	x.left = deleteMin(x.left);
	x.count = 1 + size(x.left) + size(x.right);
	return x;
}
```
#### Hibbard deletion
1. Search for the Node t containing Key key;
2. Different conditions with key:
- (key has 0 child) delete key by setting its parent to null
- (key has 1 child) delete key by link its child to its parent
- (key has 2 child) delete key by exchange itself with its right subtree's minimum
```java
public void delete(Key key){
	root = delete(root, key);
}
private Node delete(Node x, Key key){
	if(x == null) return null;
	int cmp = key.compareTo(x.key);
	if(cmp < 0) x.left = delete(x.left, key);
	else if(cmp > 0) x.right = delete(x.right, key);
	else{
		if(root.right == null) return root.left;
		if(root.left == null) return root.right;
		
		Node t = x;
		x = min(t.right);
		x.right = deleteMin(t.right);
		x.left = t.left;
	}
	x.count = size(x.left) + size(x.right) + 1;
	return x;
}
```
O(h) (h = N^0.5)




