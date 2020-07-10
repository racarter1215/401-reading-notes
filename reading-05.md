# Linked Lists

### I learned that linked lista are data structures that contains nodes that link and point to subsequent nodes.

##### I also learned that a singly is the number of references the node has, this one has only one reference, and the reference points to the Next node in a linked list.

##### Doubly, logically, refer to there being two references within the node. A Doubly linked list means that there is a reference to both the Next and Previous node.

##### Nodes are the individual parts of a linked list, like links in a chain IRL

##### "Next" is how you traverse the nodes (not a for or foreach loop, apparently). You use a while loop in tandem with Next.

##### The "Head" is the reference type of the first node

##### the "Current" is the reference type of the current node

##### Example:

##### ALGORTIHM Includes (value)
##### 		// INPUT <-- integer value
##### 		// OUTPUT <-- boolean
			
##### 			Current <-- Head

##### 			WHILE Current is not NULL
##### 				IF Current.Value is equal to value
##### 					return TRUE

##### 				Current <-- Current.Next

##### 			return FALSE

##### The while loop will only run if the node that "current" is pointing to is not null. 

##### Then check if the value of "current" is equal to the search value. If true, we return true.

##### If not, move to next node.

### Big O

##### For the above algorithm, Big O would be O(n). Big O of space would be O(1). 

##### Adding Big O(1): Set "current" to Head, then instantiate the new node to add. The values passed in as arguments into the Add() method will define what the value of the Node will be.

##### Example:

##### ALGORITHM Add(newNode)
##### 		// INPUT <-- Node to add 
##### 		// OUTPUT<-- No output

##### 			Current <-- Head
##### 			newNode.Next <-- Head
##### 			Head <-- newNode
##### 			Current <-- Head

