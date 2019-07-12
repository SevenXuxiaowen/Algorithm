# Geometric_BST
## 1d range search
#### Definition
Extension of ordered symbol table. (Always used in database query)
- Insert key-value pair
- Search key
- Delete key
- `Range search`: find all keys between k1 and k2
- `Range count`: number of keys between k1 and k2
#### BST implementation
```java
public int size(Key lo, Key hi){
    if(contains(hi)) return rank(hi) - rank(lo) + 1;
    else return rank(hi) - rank(lo);
}
```
- Recursively find all keys in the left child. (if any could fall in range)
- Check key in current node
- Recursively find all keys in the rifht child. (if any could fall in range)
#### Ranning time
Proportional to `R + lgN`
- `R` - the time that return all the nodes that fall in range
- `lgN` - the time find first node that fall in range
