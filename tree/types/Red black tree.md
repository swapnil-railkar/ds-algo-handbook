tag : #tree 

#### Introduction : 

A red black tree is a binary search tree with additional information of color stored. By constraining the node colors on any simple path from root to leaf, red black trees ensure that **no such path is more than twice as long as any other, so that the tree is approximately balanced**. A red black tree is binary search tree that satisfies following properties : 
1. Every node is either red or black.
2. The root is black.
3. Every leaf (null) node is black.
4. If node is red then both children are black.
5. For each node, all simple paths from the node to descendent leaves contains same number of black nodes.

#### Implementation : 

A node in red black tree contains data and pointer to its left child, right child and parent also attribute color. This is represented as

```
public enum Color {
	RED,
	BLACK
}

Class Node {
	int data;
	int left;
	int right;
	int parent;
	Color color;
	
	Node(int data) {
		this.data = data;
		this.color = Color.RED;
		this.left = null;
		this.right = null;
		this.parent = null;
	}
}
```

Following implementation treats _root_ as root of the tree. We can define a RedBlackTree class as

```
public class RedBlackTree {
	private Node root;
	
	RedBlackTree() {
		this.root = null;
	}
	.
	.
	.
}
```

We can insert a node in an n-node red-black tree in O(log n) time. We insert a node into tree as if it were an ordinary binary tree and then color the node red.

```
public void insert(int data) {
	Node currentRoot = root;
	Node parent = null;
	
	while(currentRoot != null) {
		parent = currentRoot;
		if(data < currentRoot.data) {
			currentRoot = currentRoot.left;
		} else {
			currentRoot = currentRoot.right;
		}
	}
	
	Node node = new Node(data);
	node.parent = parent;
	if(parent == null) {
		this.root = node;
	} else if(data < parent.data) {
		parent.left = node;
	} else {
		parent.left = node;
	}
	
	insertFixup(node);
}
```

To ensure that the red black properties are preserved, we call *insertFixup* procedure to re-color nodes and perform rotations. The loop in *insertFixup*  maintains the following three part invariant at start of each iteration of loop.
1. Node *z* is red.
2. If *z.parent* is root then *z.parent* is black.
3. If tree violates any of red black properties, it violates at most two which are either of : 
	- Property 2, because *z* is root and it is red.
	- Property 4, because *z* is and *z.parent* both are red.

To fix this, we consider following cases,
1. *z*'s uncle *y* is red : 
	This case occurs when both *z.parent* and *y* (sibling of *z.parent*) are red. To fix this, we color both *z.parent* and *y* as black and then we color *z.parent.parent* as red. We repeat the loop with *z.parent.parent* as new *z*, that is, all pointers move up two levels in the tree.
2. *z*'s uncle *y* is black and *z* is a right child 
3. *z's* uncle *y* is black and *z* is a left child
	In case 2, node *z* is right child of it's parent. We transform this case into case 3 by using left rotation on node *z* and make it left child of its parent. Because both *z* and *z.parent* were red, rotation neither affects black height of nodes not property 5.
	Whether we enter case 3 directly or via rotation, *z*'s uncle *y* is black since otherwise we would have executed case 1.
	In case 3, we execute some color changes and then perform right rotation which preserves property 5

```
private void insertFixup(Node node) {
	while(node != null && node.parent != null && node.parent.color == Color.RED) {
		if(node.parent.parent == null) {
			break;
		}
		if(node.parent == node.parent.parent.left) {
			Node uncle = node.parent.parent.right;
			if(uncle != null && uncle.color == Color.RED) {
				// case 1
				node.parent.color = Color.BLACK;
				uncle.color = Color.BLACK;
				node.parent.parent.color = Color.RED;
				node = node.parent.parent;
			} else {
				if(node == node.parent.right) {
					 // case 2
					 node = node.parent;
					 leftRotate(node);
				}
				// case 3
				node.parent.color = Color.BLACK;
				node.parent.parent.color = Color.RED;
				rightRotate(node.parent.parent);
			}
		} else {
			Node uncle = node.parent.parent.right;
			if(uncle != null && uncle.color == Color.RED) {
				// case 1 mirror
				node.parent.color = Color.BLACK;
				uncle.color = Color.BLACK;
				node.parent.parent.color = Color.RED;
				node = node.parent.parent;
			} else {
				// case 2 mirror
				if(node == node.parent.left) {
					node = node.parent;
					rightRotate(node);
				}
				// case 3 mirror
				node.parent.color = Color.BLACK;
				mode.parent.parent.color = Color.RED;
				leftRotate(node.parent.parent);
			}
		}
	}
	if(this.root != null) {
		this.root.color = Color.BLACK;
	}
}
```

following procedure replaces subtree rooted at node *u* by subtree rooted at node *v*, node *u*'s parent becomes node *v*'s parent and node *u*'s parent end up having node *v* as appropriate child.

```
private void transplant(Node nodeToReplace, Node replacementNode) {
	if(nodeToReplace.parent == null) {
		this.root = replacementNode;
	} else if(nodeToReplace = nodeToReplace.parent.left) {
		nodeToReplace.parent.left = replacementNode;
	} else {
		nodeToReplace.parent.right = replacementNode;
	}
	
	if(replacementNode != null) {
		replacementNode.parent = nodeToReplace.parent;
	}
}
```

When we want to delete node *z* and and *z* has fewer than two children then *y* (z's only child) replaces *z* in the tree. When *z* have two children, *y* becomes the leftmost node in *z*'s right subtree and *x* points to *y*'s right child. This *x* replaces *y* in tree and *y* replaces thus removing *z* from the tree.
We remember *y*'s original color before swap as it can cause violation of red black properties.

```
public void delete(int key) {
	Node node = search(key);
	if(node != null) {
		deleteRBNode(node);
	}
}

private void deleteRBNode(Node node) {
	Color originalColor = node.color;
	Node temp = null;
	if(node.left == null) {
		temp = node.right;
		transplant(nodeToReplace, temp);
	} else if(node.right == null) {
		temp = node.left;
		transplant(nodeToReplace, temp);
	} else {
		Node min = minimum(node.right);
		originalColor = min.color;
		temp = min.right;
		if(min.parent == node) {
			temp.parent = node;
		} else {
			transplant(min, temp);
			min.right = node.right;
			min.right.parent = min;
		}
		transplant(node, min);
		min.left = node.left;
		min.left.parent = min;
	}
	if(originalColor == Color.BLACK) {
		deleteFixup(root, temp);
	}
}
```


Fixup after deleting a node consider following cases : 
1. Node *x*'s sibling *w* is red :
	Since *w* must have black children, we switch colors of *w* and *x.parent* and then perform left rotation on *x.parent* without violating any red black properties.
	The new sibling of *x* which is one of *w*'s children prior rotation, is now black, thus giving us one of case 2, 3 or 4.
2. Node *x*'s sibling *w* is black and both of *w*'s children are black : 
	We recolor *w* as red and move *x* pointer up a level in tree. As *x*'s color is now red, it causes fixup procedure to stop and lastly we color new *x* to black thus maintaining all properties.
3. Node *x*'s sibling *w* is black and *w*'s left child is red and right child is black :
	We change color of *w* and its left child and then perform right rotation on *w* without violating any red black properties. The new sibling of *w* of *x* is now a black node with red right child thus giving us case 4.
4. Node *x*'s sibling *w* is black and *w*'s right child is red : 
	In this case , by making some color changes and performing a left rotation on *x*.parent we maintain red-black properties. Then we set *x* to root causing loop to terminate.


```
private void deleteFixup(Node root, Node node) {
	while(node != root && node.color == Color.BLACK) {
		if(node.parent == null) {
			break;
		}
		if(node == node.parent.left) {
			Node sibling = node.parent.right;
			if(sibling != null) {
				if(sibling.color == Color.RED) {
					// case 1
					sibling.color = Color.BLACK;
					node.parent.color = Color.RED;
					leftRotate(node.parent);
					sibling = node.parent.right;
				} 
				if((sibling.left == null && sibling.left.color == Color.BLACK) && (sibling.right == null && sibling.right.color == BLACK)) {
					// case 2
					sibling.color = Color.RED;
					node = node.parent;
				} else {
					if(sibling.right != null && sibling.right.color == Color.BLACK) {
						// case 3
						if(sibling.left != null) {
							sibling.left.color = Color.BLACK;
						}
						sibling.color = Color.RED;
						rightRotate(sibling);
						sibling = node.parent.right;
					}
					// case 4
					sibling.color = node.parent.color;
					node.parent.color = Color.BLACK;
					sibling.right.color = Color.BLACK;
					leftRotate(node.parent);
					node = this.root;
				}
			} else {
				break;
			}
		} else {
			// mirror cases
			Node sibling = node.parent.left;
			if(sibling != null) {
				// case 1 mirror
				sibling.color = Color.BLACK;
				rightRotate(node.parent);
				sibling = node.parent.left;
			}
			if((sibling.left == null && sibling.left.color == Color.BLACK) 
				&& (sibling.right == null && sibling.right.color == BLACK)) {
					// case 2
					sibling.color = Color.RED;
					node = node.parent;
				} else {
					if(sibling.left != null && sibling.left.color ==
						Color.BLACK){
						// case 3
						if(sibling.right != null) {
							sibling.right.color = Color.BLACK;
						}
						sibling.color = Color.RED;
						leftRotate(sibling);
						sibling = node.parent.left;
					}
					// case 4
					sibling.color = node.parent.color;
					node.parent.color = Color.BLACK;
					sibling.left.color = Color.BLACK;
					rightRotate(node.parent);
					node = this.root;
				}
			} else {
				break;
			}
		}
	}
	if(node != null) {
		node.color = Color.BLACK;
	}
}
```









