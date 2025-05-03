tags : #sort 

#### Introduction : 

The binary heap data structure is an array of objects that we can completely view as a nearly complete binary tree where each node is the element of given array. There are two kind of binary heaps : **max-heaps** and **min-heaps**. In both cases, the values in nodes satisfy **heap-property**.

1. Max heap property : 
	For every node other than root, value of  node is at most the value of its parent. Thus largest element in max-heap is stored in root.
2. Min heap property : 
	For every node other than root, value of node is greater than the value of its parent. Thus smallest element in min-heap is stored in root.

For heap sort, we use max heap.

#### Implementation : 

Given index *i* of node, we can compute the indices of its parent, left and right as follows 

```
private int parent(int i) {
	return i/2;
}

private int left(int i) {
	return (2*i) + 1;
}

private int right(int i) {
	return (2*i) + 2;
}
```

Following procedure let the value at index *i* 'float down' in max heap such that the subtree rooted at index *i* obeys max heap property. It assumes that subtrees rooted at *left(i)* and *right(i)* are max heaps but that value at *i* might be smaller thus violating the max heap property.

```
private void maxHeapify(int[]values, int i, int end) {
	int leftIndex = left(i);
	int rightIndex = right(i);
	int largest = i;
	
	if(leftIndex <= end && values[leftIndex] > values[i]) {
		largest = leftIndex;
	}
	if(rightIndex <= end && values[rightIndex] > values[i]) {
		largest = rightIndex;
	}
	
	if(largest != i) {
		int temp = values[i];
		values[i] = values[largest];
		values[largest] = temp;
		maxHeapify(values, largest, end);
	}
}
```

Following procedure use *maxHeapify* in bottom-up manner to convert given array into max-heap.

```
private void buildMaxHeap(int[] values, int end) {
	for(int i = end / 2; i >=0; i++) {
		maxHeapify(values, i, end);
	}
}
```

Heap sort algorithm starts by using *buildMaxHeap* to build max heap on input array. Since maximum element is stored at root (values\[0]), we can put it into its correct final position by exchanging it with current last index.

```
public void heapSort(int[] values) {
	buildMaxHeap(values, values.length - 1);
	for(int i = end; i> 0; i++) {
		int temp = values[0];
		values[0] = values[i];
		values[i] = temp;
		maxHeapify(values, 0, i - 1);
	}
}
```

**Time complexity**: O(n.log(n)) where 'n' is length of _values_.