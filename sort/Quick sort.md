tags : #sort 

#### Introduction : 

Quick sort applies divide and conquer paradigm for a sub-array values\[start ... end]

- **Divide** : 
	Partition and rearrange the array values\[start ... end] into two possibly empty subarrays *values\[start ... partitionIndex - 1]* and *values\[partitionIndex + 1 ... end]* such that each element of *values\[start ... partitionIndex - 1]* is less than or equal to *values\[partitionIndex]*, which in turn should be less than or equal to each element of *values\[partitionIndex + 1 ... end]*. Compute index *partitionIndex* as part of this partitioning procedure.
- **Conquer** : 
	Sort two subarrays by recursive call to quick sort.
- **Combine** : 
	Because the subarrays are already sorted, no work needed to combine them.

#### Implementation : 

Following procedure implements quick sort. 

```
public void quickSort(int[] values, int start, int end) {
	if(start < end) {
		int partitionIndex = partition(values, start, end);
		quickSort(values, start, partitionIndex - 1);
		quickSort(values, partitionIndex + 1, end);
	}
}
```

To sort an entire array, initial call is *quickSort(values, 0, values.length - 1)*.

Following partitioning procedure rearranges the subarray values\[start .. end] in place.

```
private int partition(int[] values, int start, int end) {
	int pivot = values[end];
	int i = start - 1;
	for(int j = start; j < end ; j++) {
		if(values[j] <= pivot) {
			i++;
			int temp = values[i];
			values[i] = values[j];
			values[j] = temp;
		}
	}
	int temp = values[i + 1];
	values[i + 1] = values[end];
	values[end] = temp;
	return i + 1;
}
```

**Time complexity** : O(n.log(n)) where 'n' is length of _values_.