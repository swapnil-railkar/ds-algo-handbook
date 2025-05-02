tags : #search 

#### Introduction : 

Binary search is effective way of searching element in given collection of element. To implement binary search, **collection should be sorted in ascending manner**. Binary search uses divide and conquer approach to search the element in collection.

#### Implementation : 

```
public int binarySearch(int[] nums, int key) {
	int start = 0;
	int end = nums.length - 1;
	while(start <= end) {
		int mid = (start + end) / 2;
		if(nums[mid] == key) {
			return mid;
		} else if(nums[mid] > key) {
			end = mid - 1;
		} else {
			end = mid + 1;
		}
	}
	return -1;
}
```

Above method shows implementation of binary search. We partition the collection in two sub-parts and validates element in middle with element to be found. As the collection is sorted, if element in middle is greater than key then key must be present in left half of collection where elements are smaller than middle element or in the right half otherwise where elements are bigger than middle element. This process continues until middle element of partitioned collection matches the key or both halves collide.

**Time complexity** : O(log(n)) where 'n' is total number of elements in collection.