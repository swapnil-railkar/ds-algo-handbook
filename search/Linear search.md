tags : #search

#### Introduction : 

Linear search is searching algorithm used to find given element in a collection of elements.

#### Implementation : 

```
public int linearSearch(int[] values, int key) {
	for(int i = 0; i< values.length; i++) {
		if(values[i] == key) {
			return i;
		}
	}
	return -1;
}
```

Above methods implements linear search. It takes as argument integer array and key to be searched in the given array. It then iterates over the array and returns index of key if key present and -1 otherwise.

**Time complexity** : O(n) where 'n' is total number of elements in collection.
