# Hash Table
## Summary of Symbol Table implementations
#### Sequential search (unordered linkedList)
| worst case | average case |
| ------ | ------ |
| search: `N` | search: `N/2` |
| insert: `N` | insert: `N` |
| delete: `N` | delete: `N/2` |
#### Binary search (ordered array)
| worst case | average case |
| ------ | ------ |
| search: `lgN` | search: `lgN` |
| insert: `N` | insert: `N/2` |
| delete: `N` | delete: `N/2` |
#### BST
| worst case | average case |
| ------ | ------ |
| search: `N` | search: `1.38lgN` |
| insert: `N` | insert: `1.38lgN` |
| delete: `N` | delete: `1.38lgN` |
#### Red-black BST
| worst case | average case |
| ------ | ------ |
| search: `2lgN` | search: `1.00lgN` |
| insert: `2lgN` | insert: `1.00lgN` |
| delete: `2lgN` | delete: `1.00lgN` |
## Hash function
#### Explination
Basically, hash table is the trade-off between space comlecity with time comlecity. Two keys that hash to the same key index is called collision. The function that convert the key to a particular index number called hash function.
#### Ideally requirement
Scrable the key uniformly to generate a table index
- Efficiently computable
- Each table index equally likely for each key.(ideally random distribution)
#### Hash code design
- Combine each significant code using `31x + y`
- If the field is a primative type, use a wrapper type hashCode()
- If the field is `null`, return 0;
- If the code is a reference type, using its hashCode() recursively;
- If the field is array, use Arrays.deepHashCode();
```java
public final class Example implements Comparable<Example>{
    private final String field1;
    private final Referece field2;
    private final double field3;
    
    public int hashCode(){
        int hash = 17;
        hash = 31*hash + field1.hashCode();
        hash = 31*hash + field2.hashCode;
        hash = 31*hash + ((Double)field3).hashCode;
    }
}
```
#### Hash code vs hash function
- `hash code`: An `int` between `2^-31` and `2^31`
- `hash function`: An `int` between `0` and `M-1` (must be positive)

## Seperate chaining
#### Definition
Two distinct keys is hashed to the same index. In practice, we deal with collision efficiently.
#### Implementation
```java
public class SeperateChainingHashST<Key, Value>{
    private int M = 97; //the number of chains M~N/5
    private Node[] st = new Node[M]; //array of chains, each chian contains a single-direction linkedList
    
    private class Node{
        private Object key;
        private Object val;
        private Node next;
        ...
    }
    
    private int hash(Key key){
        return (key.hashCode() & 0x7fffffff)%M;
    }
    
    public void put(Key key, Value val){
        int i = hash(key);
        for(Node x = st[i]; x != null; x = x.next){
            if(key.equals(x)) {x.val = val; return}
        }
        st[i] = new Node(key, val, st[i]);
    }
}
```
#### Running time
Under uniform hashing assumption, prob.(the number of keys in a list) is extremely close to 1.
| worst case | average case |
| ------ | ------ |
| search: `lgN` | search: `3-5` |
| insert: `lgN` | insert: `3-5` |
| delete: `lgN` | delete: `3-5` |






















