tags : #sort 

#### Introduction : 

Insertion sort is an efficient way for  sorting small number of elements. The algorithm sorts the input numbers in place. Insertion sort ensures that for element at index *i*, elements up to *i* are sorted. Algorithm places the element at index *i* in its appropriate place in left sub-array, shifting each element in left sub-array which is greater than key element to right along the way.

#### Implementation : 

```
public void insertionSort(int[] values) {
	for(int i = 1; i< values.length; i++) {
		key = values[i];
		j = i - 1;
		while(j >= 0 && values[j] > key) {
			values[j + 1] = values[j];
			j--;
		}
		values[j + 1] = key;
	}
}
```

**Time complexity** : O($n^2$) where 'n' is total number of elements in collection.