tags : #queue

#### Introduction : 

Queue implements **First In First Out** policy. That is, the element which is deleted is the oldest element in the queue.

#### Implementation : 

In this implementation, stack is implemented using singly linked list. Each node in stack contains data and pointer to next element in stack.

```
Class Node {
	private int data;
	private Node next;
	
	Node(int data) {
		this.data = data;
		this.next = null;
	}
	
	public int getData() {
		return this.data;
	}
	
	public Node getNext() {
		return this.next;
	}
	
	public void setNext(Node next) {
		this.next = next;
	} 
	
}
```

This implementation maintains two pointers, one to point head of list and one to point last element of list.

```
Class Queue {
	private Node head;
	private Node tail;
	
	Queue() {
		this.head = null;
		this.tail = null;
	}
	
	.
	.
	.
}
```

An element is added at the tail of queue. This operation is called as **enqueue**.

```
public void enqueue(int data) {
	if(head == null && tail == null) {
		Node node = new Node(data);
		head = node;
		tail = node;
		return;
	}
	Node node = new Node(data);
	tail.setNext(node);
	node = tail;
}
```

Following implementation shows **peek** operation, which is used to get oldest value in queue.

```
public int peek() {
	if(head == null) {
		throw new Exception("Underflow exception");
	}
	return head.getData();
}
```

In queue, oldest element is removed first. As **head** attributes points to oldest node, we remove head from queue and its successor becomes new head. This operation is called as **dequeue**.

```
public int dequeue() {
	if(head == null) {
		throw new Exception("Underflow exception");
	}
	
	int data = head.getData();
	head = head.getNext();
	return data;
}
```

