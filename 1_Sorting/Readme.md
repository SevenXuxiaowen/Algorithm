
# Sorting
## Sort API
The ```interface``` in java is like the callback function in Javascript, a reference to exacutable code.
### Comparable interface (build-in Java interface)
```java
public interface Comparable<Item>{ 
  public int compareTo(Item that); 
}
```
### Build a class that implements Comparable interface
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
	private static boolean less(Comparable v, Comparable w){ return v.compareTo(w) < 0; }

	private static void exch(Comparable[] a, int i, int j){
		Compareble temp = a[i];
		a[i] = a[j];
		a[j] = temp;
	}

	private static boolean isSorted(Comparable[] a){
		for (int i = 1; i < a.length; i++){ if(less(comparable[i], comparable[i - 1])) return false; }
		return true;
	}


	//Different sortings
	public static void sort(Comparable[] a){
		//TODO:SORTING ALGORITHM
	}
}
```
## Selection Sort
Iterite array, for each iteration a[i], find the min element in the right entries of a[i]. Then, exchage a[i] and a[min].
```java
publich static void sort(Comparable[] a){
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
## Merge Sort (recursion)
## Merge Sort (bottom-up)
## Quick Sort
