# Stacks and Queues

### Stack: data structure that consists of Nodes. Nodes only reference next node, not previous.

##### Push: Nodes or items that are put into the stack are pushed
##### Pop: Nodes or items that are removed from the stack are popped. 
##### Top: Top of the stack.
##### Peek: View the value of the top Node in the stack. 
##### IsEmpty: returns true when stack is empty.

##### FILO: First in last out, the first item added in the stack will be the last item out
##### LIFO: Last in first out, the last item added to the stack will be the first item out

##### Push: will always be an O(1) operation. 
##### Example:
##### ALOGORITHM push(value)
##### // INPUT <-- value to add, wrapped in Node internally
##### // OUTPUT <-- none
#####    node = new Node(value)
#####    node.next <-- Top
#####    top <-- Node

##### Popping a Node off a stack removes the Node from the top.
##### Example:
##### ALGORITHM pop()
##### // INPUT <-- No input
##### // OUTPUT <-- value of top Node in stack
##### // EXCEPTION if stack is empty

#####    Node temp <-- top
#####    top <-- top.next
#####    temp.next <-- null
#####    return temp.valueThis means that the last item in the queue will be the last item out of the queue.

### Queue Examples:
##### Enqueue: Nodes or items that are added to the queue.
##### Dequeue: Nodes or items that are removed from the queue.
##### Front: first Node of the queue.
##### Rear: last Node of the queue.
##### Peek: view the value of the front Node in the queue.
##### IsEmpty: returns true when queue is empty.

##### FIFO: First in first out, the first item in the queue will be the first item out
##### LILO: Last in last out, the last item in the queue will be the last item out
