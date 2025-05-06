tags : #linkedList

#### Introduction : 

A linked list is a data structure in which the objects are arranged in a linear order. Unlike an array, in which the linear order is determined by the array indices, the order in linked list is determined by a pointer in each object. 
Linked list is list of nodes where each *node* contains a key and pointer to next node in list. If pointer to next node is null then it is the last element of list. Linked list have attribute *head* which points to first element of list and is a sole entry point of list. If *head* is null then list is empty. Following implementation shows CRUD operations on linked list.

#### Implementation : 

In linked list, each node contains a *key* which can be of any data type and pointer to next node in list.

```
Class Node {
	private int key;
	private Node next;
	
	Node(int key) {
		this.key = key;
		this.next = null;
	}
	
	public int getKey() {
		return key;
	}
	
	public void setKey(iny key) {
		this.key = key;
	}
	
	public Node getNext() {
		return next;
	}
	
	public void setNext(Node next) {
		this.next = next;
	}
}
```

Data is inserted at tail of list. Following procedure adds new data in list

```
public Node insert(Node head, int key) {
	if(head == null) {
		return new Node(key);
	}
	
	Node currentNode = head;
	while(currentNode.getNext() != null) {
		currentNode = currentNode.getNext();
	}
	Node node = new Node(key);
	currentNode.setNext(node);
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

We delete a node by updating the previous node’s successor to point to the successor of the node being deleted.

```
public void delete(Node head, int key) {
	if(head.getKey() == key) {
		head = head.getNext();
		return;
	}
	
	Node currentNode = head;
	while(currentNode.getNext() != null 
			&& currentNode.getNext().getKey() != key) {
		currentNode = currentNode.getNext();
	}
	
	if(currentNode.getNext() != null) {
		currentNode.setNext(currentNode.getNext().getNext());
	}
}
```

Following procedure updates given key with new key.

```
public void update(Node head, int key, int updatedKey) {
	Node node = search(head, key);
	node.setKey(updatedKey);
}
```

