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
## Implement equals() for 2 key
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
