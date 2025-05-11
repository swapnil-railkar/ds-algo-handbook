tags : #tree 

#### Introduction :

An AVL (Adelson-Velsky and Evgenii Landis, soviet mathematicians) tree is defined as self balancing binary search tree where the differences between heights of left and right subtrees for any node cannot be more than one. The difference between heights of left subtree and right subtree is known as balance factor of node.


#### Implementation : 

A node in binary search tree contains data and pointer to its left child, right child and parent as well as its height. This is represented as

```
Class Node {
	int data;
	int height;
	Node left;
	Node right;
	
	Node(int data) {
		this.data = data;
		this.height = 1;
	}
}
```

Following implementation treats _root_ as root of the tree. We can define a AVL class as

```
Class AVL {
	private Node root;
	
	AVL() {
		this.root = null;
	}
	.
	.
	.	
}
```

Following method is used to get balance factor of given node.

```
private int getBalanceFactor(Node node) {
	return (node == null) ? 0 : height(node.left) - height(node.right);
}

private int height(Node node) {
	return (node == null) ? 0 : node.height;
}
```

Following procedure updates the height of given node

```
private void updateHeight(Node node) {
	node.height = 1 + Math.max(height(node.left), height(node.right));
}
```

Following procedures are wrappers for rotation to update rotated node's height after rotation

```
private Node leftRotateWithHeightUpdate(Node node) {
	Node newRoot = leftRotate(node);
	updateHeight(node);
	updateHeight(newRoot);
	return newRoot;
}

private Node rightRotateWithHeightUpdate(Node node) {
	Node newRoot = rightRotate(node);
	updateHeight(newRoot);
	updateHeight(node);
	return newRoot;
}
```

Following procedure is responsible with balancing the node if it is unbalanced

```
private Node balance(Node node) {
	int balanceFactor = getBalanceFactor(node);
	
	if(balanceFactor > 1) {
		if(getBalanceFactor(node.left) < 0) {
			node.left = leftRotateWithHeightUpdate(node.left)
		}
		return rightRotateWithHeightUpdate(node);
	}
	if(balanceFactor < -1) {
		if(getBalanceFactor(node.right) > 0) {
			node.right = rightRotateWithHeightUpdate(node.right);
		}
		return leftRotateWithHeightUpdate(node);
	}
	return node;
}
```

New node is added as leaf node. It follows insertion procedure of binary search tree with balancing fixes.

```
public void insert(int data) {
	root = insert(root, data);
}

private Node insert(Node node, int data) {
	if(node == null) {
		return new Node(data);
	}
	
	if(data < node.data) {
		node.left = insert(node.left, data);
	} else {
		node.right = insert(node.right, data);
	}
	updateHeight(node);
	return balance(node);
}
```

Deleting in AVL tree follows same approach as BST with balancing changes

```
public void delete(int key) {
	root = delete(root, key);
}

private Node delete(Node node, int key) {
	if(node == null) {
		return null;
	}
	if(key < node.data) {
		node.left = delete(node.left, key);
	} else if(key > node.data) {
		node.right = delete(node.right, key);
	} else {
		if(node.left == null || node.right == null) {
			node = (node.left != null) ? node.left : node.right;
		}  else {
			Node min = minimum(node.right);
			node.key = min.key;
			node.right = delete(node.right, min.key);
		}
	}
	if(node == null) {
		return null;
	}
	updateHeight(node);
	return balance(node);
}
```

