tags : #tree 

#### Introduction : 

Binary tree traversals involve visiting each node in a tree structure in specific order. Depending on how we visit the *root* there are mainly three types of binary tree traversals.
1. **Inorder traversal** : 
	In this traversal we first visit root's left subtree first then we visit root node itself and then proceed to visit right subtree.
2. **Preorder traversal** : 
	In this traversal we first visit the root node, then we traverse left subtree and finally the right subtree.
3. **Postorder traversal** :
	In this this traversal, we first visit a node's left subtree then we visit node's right subtree and then we visit the node itself.

#### Implementation : 

```
public void inorder(Node root) {
	if(root != null) {
		inorder(root.left);
		System.out.println(root.data); // visit the node and process data.
		inorder(root.right);
	}
}

public void preorder(Node root) {
	if(root != null) {
		System.out.println(root.data);
		preorder(root.left);
		preorder(root.right);
	}
}

public void postorder(Node root) {
	if(root != null) {
		postorder(root.left);
		postorder(root.right);
		System.out.println(root.data);
	}
}
```

