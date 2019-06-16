# Sorting
[create an anchor](#sort-api)
## Sort API
The ```interface``` in java is like the callback function in Javascript, a reference to exacutable code.
#### Comparable interface (build-in Java interface)
```java
public interface Comparable<Item>{ 
    public int compareTo(Item that); 
}
```
#### Build a class that implements Comparable interface
```java
public class SelfDefineClass implements Comparable<Item>{
    /** initialize */
    /** Constructor */
    public SelectionSort(){ }

    //implements interface
    public int comparaTo(Item that){
        if(condition1) return -1;
        if(condition2) return 0;
        if(condition3) return 1;
    }

    //Helper functions
    private static boolean less(Comparable v, Comparable w){ 
        return v.compareTo(w) < 0; 
    }

    private static void exch(Comparable[] a, int i, int j){
        Compareble temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }

    private static boolean isSorted(Comparable[] a){
        for (int i = 1; i < a.length; i++){ 
            if(less(comparable[i], comparable[i - 1])) return false; 
        }
        return true;
    }


    //Different sortings
    public static void sort(Comparable[] a){
        //TODO:SORTING ALGORITHM
    }
}
```
## Selection Sort
Iterate array, for each iteration a[i], find the min element in the right entries of a[i]. Then, exchage a[i] and a[min].
```java
public static void sort(Comparable[] a){
    int N = a.length;
    for(int i = 0; i < N; i++){
        int min = i;
        for(int j = i + 1; j < N; j++){
            if(less(a[j], a[min])) min = j;
        }
        exch(a, i, min);
    }
}
```
## Insertion Sort
Iterate array, for every iteration a[i], compare itself to its every left entry. When it meete element that bigger that it, exchange them, untill it meets the first elemen that "smaller" that it.
```java
public static void sort(Comparable[] a){
    int N = a.length;
    for(int i = 0; i < N; i++){
        for(int j = i; j > 0; j--){
            if(less(a[j], a[j-1])) exch(a, j, j-1)
            else break;
        }
    }
}
```
## Merge Sort (recursion)
1. Divid a array to 2 part in the middle. We assume that partrition A and partrition B has been sorted, so after merging the 2 array, the whole array is sorted;
2. Sort the 2 parts in a recurtion way.
```java
private static void merge(Comparable[] a, Comparable[] aux, int lo, int mid, int hi){
    //Step 1: Copy elements of a into aux
    for(int k = lo; k <= hi; k++){
        aux[k] = a[k];
    }
    //Step 2: merge
    int i = lo, j = mid + 1;
    for(int k = lo; k <= hi; k++){
        if(i > mid)                   a[k] = aux[j++];
        else if(j > hi)               a[k] = aux[i++];
        else if(less(aux[j], aux[i])) a[k] = aux[j++];
        else                          a[k] = aux[i++];
    }
}
private static void sort(Comparable[] a, Comparable[] aux, int lo, int hi){
    if(lo <= hi) return;
    int mid = lo + (hi - lo) / 2;
    sort(a, aux, lo, mid);
    sort(a, aux, mid + 1, hi)
    if(!less(a[mid + 1], a[mid]) return;
    merge(a, aux, lo, mid, hi);
}
public static void sort(Comparable[] a){
    Comparable[] aux = new Comparable[a.length];
    sort(a, aux, 0, a.length - 1);
}
```
## Merge Sort (bottom-up)
```Java
private static void merge(Comparable[] a, Comparable[] aux, int lo, int mid, int hi){
    for(int k = lo; k <= hi; k++){
        aux[k] = a[k];
    }
    int i = lo, j = mid + 1;
    for(int k = lo; k <= hi; k++){
        if(i > mid)                   a[k] = aux[j++];
        else if(j > hi)               a[k] = aux[i++];
        else if(less(aux[i], aux[j])) a[k] = aux[i++];
        else                          a[k] = aux[j++];
    }
}
public static void sort(Comparable[] a){
    int N = a.length;
    Comparable[] aux = new Comparable[N];
    for(int sz = 1; sz < N; sz *= 2){
        for(int lo = 0; lo < N - sz; lo = lo + 2 * sz){
            merge(a, aux, lo, lo + sz - 1, Math.min(lo + s * sz - 1, N - 1));
        }
    }
}
```
## Quick Sort
1. Shuffle the array;
2. Partrition for a[j], elements on its left is no larger than a[j], elements on its right is no smaller that a[j];
3. Sort the 2 sides of the partrition recursively.
```java
private static int partrition(Comparable[] a, int lo, int hi){
    int i = lo, j = hi + 1;
    while(true) {
        while(less(a[++i], a[lo]){
            if(i == hi) break;
        }
        while(less(a[lo], a[--j]){
            if(j == lo) break;
        }
        if(i >= j) break;
        exch(a, i, j);
    }
    exch(a, lo, j);
    return j;
}

private static void sort(Comparable[] a, int lo, int hi){
    if(hi <= lo) return;
    int j = paetrition(a, lo, hi);
    sort(a, lo, j - 1);
    sort(a, j + 1, hi);
}

public static void sort(Comparable[] a){
    knuthShuffle(a);
    sort(a, 0, a.lenth - 1);
}

```
## Knuth Shuffle Demo
1. In iteration i, pick integer r between [0, i] uniformly at random;
2. Swape a[i] and a[r].
```java
public class SelfDefineClass{
    public static void knuthShuffle(Object[] a){
        int N = a.length;
        for(int i = 0; i < N; i++){
            int r = Math.randomNumber(0, i + 1) //Generate a random integer within [0, i]
            exch(a, i, r);
        }
    }
}
```
## Quick-select
#### Problem description
Given an array of N items, find a Kth smallest item.
#### Solution
Entry[j] is inplace. no larger entry to the left of a[j], no smaller entry to the right of a[j]. Implementation:
1. Recursively partrition, until the return number k of partrition equals j.
2. If k < j, partrition lo = k + 1; If k > j. partrition hi  = j - 1.
```java
public static Comparable quickSelect(Comparable[] a, int k){
    knuthShuffle(a);
    int lo = 0, hi = a.lenth - 1;
    while(lo < hi){
        int j = partrition(a, lo, hi);
        if (j < k) lo = j + 1;
        else if (j > k) hi = j - 1;
        else return a[k];
    }
    return a[k];
}
```
## Dijkstra 3-way partitioning
When there are significant number of dupliment elements in the array. Implementation:
1. v is partitioning item a[lo]
2. Iterate i from left to right:
    if (a[i] < v) throw a[i] to the left of i (exch a[lt] with a[i], increment lt and i);
    if (a[i] > v) throw a[i] to the rigght of i (axch a[ht] with a[i], decrement lo);
    if (a[i] = v) increment i
3. Recursively partrition lo -> lt, and ht -> hi.
```java
public static void sort(Comparable[] a, lo, hi){
    // Step 1, partitioning
    if(hi <= lo) return;
    int lt = lo, ht = hi;
    Comparable v = a[lo];
    int i = lo;
    while(i < gt){
        int cmp = a[i].compareTo(v);
        if(cmp < 0) exch(a, lt++, i++);
        else if(cmo > 0) exch(a, i, ht--);
        else i++;
    }
    // Step 2, recursion
    sort(a, lo, lt - 1);
    sort(a, ht + 1, hi);
}
```
