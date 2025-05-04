tags : #sort 

#### Introduction : 

Selection sort sorts an array by repeatedly selecting the smallest element from the unsorted portion and swapping it with first unsorted element. This process continues util entire array is sorted.

#### Implementation : 

```
public void selectionSort(int[] values) {
	for(int i = 0; i< values.length - 1; i++) {
		int minIndex = i;
		for(int j = i + 1; j< values.length; j++) {
			if(arr[j] <= arr[minIndex]) {
				minIndex = j;
			}
		}
		int temp = arr[i];
		arr[i] = arr[minIndex];
		arr[minIndex] = arr[i];
	}
}
```

**Time complexity** : O($n^2$) where 'n' is length of _values_.