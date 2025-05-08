tags : #linkedList 

#### Introduction : 

A doubly linked list is list of nodes where each *node* contains a key and pointer to its successor and a pointer to its predecessor. If a *node* has no predecessor then it is considered as *head* of list. If *node* has no successor then it is considered as *tail* of list. Doubly linked list have attribute *head* which points to first element of list and is a sole entry point of list. If *head* is null then list is empty. Following implementation shows CRUD operations on linked list.

#### Implementation : 

In doubly linked list, each node contains a *key* which can be of any data type and pointer to next node as well as previous node in list.

```
Class Node {
	private int key;
	private Node next;
	privare Node previous;
	
	Node(int key) {
		this.key = key;
		this.next = null;
		this.previous = null;
	}
	
	public int getKey() {
		return this.key;
	}
	
	public int setKey(int key) {
		this.key = key;
	}
	
	public Node getNext() {
		return this.next;
	}
	
	public void setNext(Node next) {
		this.next = next;
	}
	
	public Node getPrevious() {
		return this.previous;
	}
	
	public void setPrevious(Node previous) {
		this.previous = previous;
	}
}
```

Data is inserted at tail of list. Following procedure adds new data in list

```
public Node insert(Node head, int key) {
	if(head == null) {
		return new Node(key);
	}
	
	Node node = new Node(key);
	Node currentNode = head;
	while(current.getNext() != null) {
		currentNode = currentNode.getNext();
	}
	currentNode.setNext(node);
	node.setPrevious(currentNode);
	return head;
}
```

Searching of key in linked list starts from head node. We return node for which the key matches or return null otherwise.

```
public Node search(Node head, int key) {
	Node currentNode = head;
	while(currentNode != null && currentNode.getKey() != key) {
		currentNode = currentNode.getNext();
	}
	return currentNode;
}
```

If the node to delete is not the first or last node, update the next pointer of the previous node to point to the next node, and the previous pointer of the next node to point to the previous node. If the node to delete is the first node, then update the head pointer to point to the next node. If the node to delete is the last node, then update the tail pointer to point to the previous node.

```
// delete node from list
```

Following procedure updates given key with new key.

```
public void update(Node head, int key, int updatedKey) {
	Node node = search(head, key);
	node.setKey(updatedKey);
}
```


