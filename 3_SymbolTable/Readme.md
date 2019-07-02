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
| Implementations   | search | insert/delete | min/max | floor/ceiling | rank | select | ordered iteration |
| ----------------- |:------:| :------------:|:-------:|:-------------:|:----:|:------:|:-----------------:|
| Sequential search |N       | N             |N        |N              |N     |N       |NlgN               |
| Binary search     |lgN     | N             |1        |lgN            |lgN   |1       |N                  |












