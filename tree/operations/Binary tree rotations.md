tags : #tree 

#### Introduction : 

Binary tree rotations are used in self balancing binary search trees like AVL trees or Red black trees. A binary tree rotation helps in maintaining the balance of tree by restructuring the nodes. The most common types of rotations are : 
1. **Right rotation**
2. **Left rotation**
3. **Left - Right rotation**
4. **Right - Left rotation**

#### Implementation : 

1. **Right rotation** : 
	- Used when the left subtree of a node is too heavy.
	- The left child becomes the new root of the subtree and original root becomes right child of new root.
	
```
public Node rightRotate(Node pivot) {
	Node newRoot = pivot.left; // left child of pivot is new root.
	Node temp = leftNode.right;
	
	// perform rotation
	newRoot.right = pivot;
	pivot.left = temp;
	
	// update parent references.
	if(temp != null) {
		temp.parent = pivot;
	}
	newRoot.parent = pivot.parent;
	if(pivot.parent == null) {
		root = newRoot;
	} else if(pivot == pivot.parent.left) {
		pivot.parent.left = newRoot;
	} else {
		pivot.parent.right = newRoot;
	}
	pivot.parent = newRoot;
	return newRoot;
}
```

2. **Left rotation**:
	- Used when right subtree of a node is too heavy.
	- The right child of root becomes new root and original root becomes left child of new root.

```
public Node rightRotate(Node pivot) {
	Node newRoot = pivot.right;
	Node temp = newRoot.left;
	
	newRoot.left = pivot;
	pivot.right = temp;
	
	if(temp != null) {
		temp.parent = pivot;
	}
	newRoot.parent = pivot.parent;
	if(pivot.parent == null) {
		root = newRoot;
	} else if(pivot == pivot.parent.left) {
		pivot.parent.left = newRoot;
	} else {
		pivot.parent.rigth = newRoot;
	}
	pivot.parent = newRoot;
	return newRoot;
}
```

3. **Left-right rotation** : 
	- First we perform a **left rotation** on left child of node
	- After that, we perform a **right rotation** on the node.
	- This is used when left child has right heavy subtree.

```
public void leftRightRotate(Node pivot) {
	pivot.left = leftRotate(pivot.left);
	rightRotate(pivot);
}
```

4. **Right-left rotation** : 
	- First we perform a **right rotation** on right child of node.
	- After that, we perform **left rotation** on the node.
	- This is used when right child has right heavy subtree.

```
public void rightLeftRotate(Node pivot) {
	pivot.right  = rightRotate(pivot.right);
	leftRotate(pivot);
}
```


