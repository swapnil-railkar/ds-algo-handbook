tags : #tree

#### Introduction : 

A binary search tree is organized in a binary tree structure. We can represent such a tree using linked list in which each node is an object. A binary tree node contains key, which holds the data and pointer to its left and right child and parent. If child or parent is missing then appropriate pointer is *null*.
The keys in a binary search tree are always stored in such a way that it satisfies binary search tree property. Let *x* be a node in binary search tree. If *y* is a node in left subtree of *x* then *y.key* <= *x.key*.
If *y* is a node in right subtree of of *x* then *y.key* > *x.key*.
A node with no parent is called *root* of tree and is entry point of given tree. A node with no child nodes is called as *leaf* node.

#### Implementation : 

A node in binary search tree contains data and pointer to its left child, right child and parent. This is represented as 

```
Class Node {
	int data;
	Node left;
	Node right;
	Node parent;
	
	Node(int data) {
		this.data = data;
		this.left = null;
		this.right = null;
		this.parent = null;
	}
}
```

Following implementation treats *root* as root of the tree. We can define a BST class as 

```
Class BST {
	private Node root;
	
	BST() {
		this.root = null;
	}
	.
	.
	.
}
```

A node in tree is inserted as **leaf node**. Following procedure starts at root and moves downward looking for *null* to replace with input data.

```
public void insert(int value) {
	Node parent = null;
	Node currentRoot = root;
	
	while(currentRoot != null ) {
		parent = currentRoot;
		if(value < currentRoot.value) {
			currentRoot = currentRoot.left;
		} else {
			currentRoot = currentRoot.right;
		}
	}
	
	Node node = new Node(value);
	node.parent = parent;
	if(parent == null) {
		root = node;
	} else if(node.value < parent.value) {
		parent.left = node;
	} else {
		parent.right = node;
	}
}
```

Given a key, **search** returns a pointer a node with *data* as key if it exists or *null* otherwise.

```
public Node search(int key) {
	Node currentRoot = root;
	return searchKey(key, currentRoot);
}

private Node searchKey(int key, Node root) {
	if(root == null || root.data == key) {
		return root;
	}
	if(key < root.data) {
		return search(key, root.left);
	} else {
		return search(key, root.right);
	}
}
```

Due binary search tree property, leftmost node in tree contains smallest value and rightmost node in tree contains largest value

```
public Node minimum(Node root) {
	while(root != null) {
		root = root.left;
	}
	return root;
}

public Node maximum(Node root) {
	while(root != null) {
		root = root.right;
	}
	return currentRoot;
}
```

The overall strategy for deleting a node *z* from binary search tree has three basic cases 
1. If *z* has no children then we remove it by modifying its parent to replace *z* as *null* as its child.
2. If *z* has just one child then we elevate that child to take z's position in the tree by modifying *z*'s parent to replace *z* by *z*'s child.
3. If *z* has two children , then we find *z*'s successor *y* which should be in *z*'s right subtree and have *y* take *z*'s position in the tree. The rest of *z*'s original right subtree becomes *y*'s new right subtree and *z*'s left subtree becomes *y*'s left subtree. In this case we first replace *y* by its own right child and then we replace *z* by *y*.

In order to move subtrees around within the binary search tree, we use following subroutine. It replaces one subtree as a child of its parent with another subtree. When it replaces subtree rooted at node *u* with subtree rooted at node *v*, node *u*'s parent becomes node *v*'s parent and *u*'s parent ends up having *v* as its appropriate subtree.

```
private void transplant(Node nodeToReplace, Node replacementNode) {
	if(nodeToReplace == null) {
		this.root = replacementNode;
	} else if(nodeToReplace == nodeToReplace.parent.left) {
		nodeToReplace.parent.left = replacementNode;
	} else {
		nodeToReplace.parent.right = replacementNode;
	}
	
	if(replacementNode != null) {
		replacementNode.parent = nodeToReplace.parent;
	}
}
```

Following procedure deletes a node binary search tree.

```
public void delete(int key) {
	Node node = search(key);
	if(node != null) {
		deleteNode(node);
	}
}

private void deleteNode(Node node) {
	if(node.left == null) {
		transplant(node, node.right);
	} else if(node.right == null) {
		transplant(node, node.left);
	} else {
		Node min = minimum(node.right);
		if(min.parent != node) {
			tranplant(min, min.right);
			min.right = z.right;
			min.right.parent = min;
		}
		transplant(node, min);
		min.left = node.left;
		min.left.parent = min;
	}
}
```
