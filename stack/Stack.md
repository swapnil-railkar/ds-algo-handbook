tags : #stack

#### Introduction : 

Stack implements **Last In First Out** policy that is, in stack, the element deleted which is deleted is the one most recently inserted.

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

This implementation treats head of list as top of stack. We can define stack class as 

```
Class Stack {
	private Node head;
	
	Stack() {
		this.head = null;
	}
	
	.
	.
	.
}
```

An element is added to top stack. This operation is called as **push** operation. In linked list operation, we treat head as top of stack hence new element becomes head of list.

```
public void push(int data) {
	Node node = new Node(data);
	node.next = head;
	node = head;
}
```

Following implementation shows **peek** operation, which is used to get value at top of stack.

```
public int peek() {
	if(head == null) {
		throw new Exception("Underflow exception");
	}
	return head.data;
}
```

An element is removed from top of stack. This operation is called as **pop** operation. In following implementation, head is removed from list and its successor becomes new head

```
public int pop() {
	if(head == null) {
		throw new Exception("Underflow exception");
	}
	
	int data = head.data;
	head = head.next;
	return data;
}
```


