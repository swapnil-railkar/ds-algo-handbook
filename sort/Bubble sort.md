tags : #sort

#### Introduction : 

Bubble sort is a popular but inefficient way of sorting collection of elements in place. It works by repeatedly swapping adjacent elements that are out of order.

#### Implementation : 

```
public void bubbleSort(int[] values) {
	for(int i = 0; i< values.length; i++) {
		for(int j = values.length - 2; j>= i; j--) {
			if(values[j] < values[j - 1]) {
				int temp = values[j];
				values[j] = values[j - 1];
				values[j - 1] = temp;
			}
		}
	}
}
```

**Time complexity** : O($n^2$) where 'n' is length of *values*.

