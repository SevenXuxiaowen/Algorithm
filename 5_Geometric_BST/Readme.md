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

# 2d orthogonal range search (KD Tree)
#### Definition
Extension of ordered symbal table to 2d keys
- Insert a 2d key
- Delete a 2d key
- Search for a 2d key
- `Range search`: find all keys that lie in a 2d range
- `Range count`: number of keys that lie n a 2d range
## Grid algorithm
#### Implementation
- Divid space into M x M grid of squres, built it into a M x M 2d array.
- Creat a linckedList of points contains in each squres
- Range search: examine only squres that intersect 2d range query
#### Running time of pint examine
- Space: M^2 + N
- Time: 1 + N/M^2 per squre examined, on average
- Trade off: `M = N^0.51`
#### Running time of range search 
if `M = N^0.51`, `R` pints in the range, and evenly distribution
- Initialize data structure - `N`
- Insert point - `1` (because it's a linked list, like a hashtable)
- Range search - `1` per point in range 
- (`R` in the range, so the grid number that intersect with range is around `x = (M^2)*(R/N)`)
- (Every grid has `y = N/M^2` pints, the total number of query is y mutiple grid number `x * y`)
- (`x*y = (M^2)*(R/N)*(N/M^2) = R`, so `R/R=1`per point in range.
## 2d tree construction
Recursively partrition plane into 2 halfplanes, save to BST
- even level : vertical line, left point goes left, right point goes right
- odd level: horizintal line, lower point goes left, upper point goes right
#### Range search in a 2d tree demo
Find all points in a rectangle range.
- Check if points in node lies in the range - `R`
- Recursively search left/bottom (if any could fall in range) - ave case: `logN`, worst case: `N^0.5`
- Recursevely search right/top (if any could fall in range) - ave case: `logN`, worst case: `N^0.5`
Running time.
- Typical case - `R + logN`
- Worst case - `R + N^0.5`













