# Trees

### Definition List:

##### Node: The individual item or dta that makes up the data structure
##### Root: The first(top) Node in the tree
##### Left Child: The node that is positioned to the left of a root or node
##### Right Child: The node that is positioned to the right of a root or node
##### Edge: The link between a parent and child node
##### Leaf: A node that does not contain any children
##### Height: The number of edges from the root to the bottommost node

##### Traversals: How one goes through a node tree

##### Depth First: where we prioritize going through the height of the tree first. 
##### Examples:
Pre-order: root >> left >> right
In-order: left >> root >> right
Post-order: left >> right >> root

##### Calling preOrder for the first time will result in the root being added to the call stack:
##### Pseudo Code Examples:
ALGORITHM preOrder(root)
// INPUT <-- root node
// OUTPUT <-- pre-order output of tree node's values

    OUTPUT <-- root.value

    if root.left is not Null
        preOrder(root.left)

    if root.right is not NULL
        preOrder(root.right)
In-order
ALGORITHM inOrder(root)
// INPUT <-- root node
// OUTPUT <-- in-order output of tree node's values

    if root.left is not NULL
        inOrder(root.left)

    OUTPUT <-- root.value

    if root.right is not NULL
        inOrder(root.right)
Post-order
ALGORITHM postOrder(root)
// INPUT <-- root node
// OUTPUT <-- post-order output of tree node's values

    if root.left is not NULL
        postOrder(root.left)

    if root.right is not NULL
        postOrder(root.right)

    OUTPUT <-- root.value
    
##### Breadth First: iterates through the tree by going through each level of the tree node-by-node.
##### Example:
ALGORITHM breadthFirst(root)
// INPUT  <-- root node
// OUTPUT <-- front node of queue to console

  Queue breadth <-- new Queue()
  breadth.enqueue(root)

  while breadth.peek()
    node front = breadth.dequeue()
    OUTPUT <-- front.value

    if front.left is not NULL
      breadth.enqueue(front.left)

    if front.right is not NULL
      breadth.enqueue(front.right)
      
##### Binary Trees: restrict the number of children to two, which are the LEFT and RIGHT
