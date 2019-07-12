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
#### Running time
Proportional to `R + lgN`
- `R` - the time that return all the nodes that fall in range
- `lgN` - the time find first node that fall in range

## Orthogonal line segment intersection
#### Definition
Given N horizontal and vertical line segments, find all intersections.
- Quadratic time implementation: Check all pairs of segment for intersections.
- Nondegeneracy assumption: all x- and y- coordinates are distinct.
#### Sweep line algorithm
Define a BST, only store the y- coordinate that have the intersection with the event v line.
- x coordinates (maybe a x direction loop) define events
- `Event`: h-segment (left endpoint): insert y-coordinate into BST
- `Event`: h-segment (right endpoint): remove y-coodinate into BST
- `Event`: v-segment: 1d range search for y endpoints
#### Running time
Proportional to `NlgN + R`
- Put x- coordinates on a PQ (or a sort) to loop event - `NlgN`
- Insert y- coordinates into BST - `NlgN`
- Delete y- coordinates into BST - `NlgN`
- Range search in BST - `NlgN + R`
