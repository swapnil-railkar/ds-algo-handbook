tags : #sort 

#### Introduction : 

Merge sort algorithm closely follows divide and conquer paradigm. Intuitively, it operates as follows 
**Divide** : Divide the n-element sequence to be sorted into two sub-sequences of $n/2$ elements each.
**Conquer** : Sort two subsequences recursively using merge sort.
**Combine** : Merge two sorted subsequences to produce sorted answer.
The recursion bottoms out when sequence to be sorted has length 1, in this case no work should be done as every sequence of length 1 is already sorted. 

We merge by calling an auxiliary procedure *merge(values, start, mid, end)*, where *values* is integer array and *start*, *mid*, *end* are indices into array such that *start* <= *mid* < *end*. The procedure assumes that the sub-arrays *values\[start ... mid]* and *values\[mid + 1 ... end]* are sorted. It merges them to form a single sorted subarray that replaces the current sub-array *values\[start ... end]*.

#### Implementation : 

```
public void mergeSort(int[] values, int start, int end) {
	if(start < end) {
		int mid = (start + end) / 2;
		mergeSort(values, start, mid);
		mergeSort(values, mid + 1, end);
		merge(values, start, mid, end);
	}
}
```

```
private void merge(int[] values, int start, int mid, int end) {
	int leftSize = mid - start + 1;
	int rightSize = end - mid;
	int[] left = new int[leftSize + 1];
	int[] right = new int[rightSize + 1];
	
	for(int i = 0; i< leftSize; i++) {
		left[i] = values[start + i];
	}
	
	for(int i = 0; i< rightSize; i++) {
		right[i] = values[mid + 1 + i];
	}
	
	left[leftSize] = Integer.MAX_VALUE;
	right[rightSize] = Integer.MAX_VALUE;
	
	int leftIndex = 0;
	int rightIndex = 0;
	
	for(int i = start; i<= end; i++) {
		if(left[leftIndex] <= right[rightIndex]) {
			values[i] = left[leftIndex];
			leftIndex++;
		} else {
			values[i] = right[rightIndex];
			rightIndex++;
		}
	}
}
```

**Time complexity** : O($n .log(n)$) where 'n' is total number of elements in collection.





