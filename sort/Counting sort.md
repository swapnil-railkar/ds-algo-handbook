tags : #sort 

#### Introduction : 

Counting sort determines for each input elements x, the number of elements less than x. It uses this information to place element x directly into its position in the output array. For example, if 17 elements are less than x, then x belongs in output position 18. We must modify this scheme slightly to handle the situation in which several elements have same values.

#### Implementation : 

Procedure assumes that the input is an array *values\[1 ... n]* and thus *values.length* = n. We require two other arrays, the array *output\[1 ... n]* holds the sorted output. The array *count\[1 ... n]* provides temporary working storage. We assume that each of the n input elements is an integer in range 0 to *range*.

```
public void countingSort(int[] values, int[] output, int range) {
	int[] count = new int[range + 1];
	
	for(int i = 0; i< values.length; i++) {
		count[values[i]] = count[values[i]] + 1;
	}
	
	for(int i = 1; i<= range; i++) {
		count[i] = count[i] + count[i - 1];
	}
	// count[i] now contain the number of elements less than of equal to i.
	
	for(int i = values.length - 1; i>=0; i--) {
		output[count[values[i]] - 1] = values[i];
		count[values[i]] -= 1;
	}
}
```

**Time complexity** : O(n) where 'n' is length of _values_.

