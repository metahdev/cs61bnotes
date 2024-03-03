An Abstract Data Type (ADT) is defined only by its operations, not by its implementation.

- Note: Interfaces in Java aren't purely abstract as they can contain some implementation details, e.g. default methods

### Binary Search Trees
One of the most important concepts in Computer Science.

First, let's start with a funny implementation of a Set using SortedLinkedList.

Fundamental Problem: Slow search (for contains method), even though it's in order.
- Move pointer to middle and flip left links. Halved search time! 

A better idea: move that pointer to the middle of the left/right part.
![[binarysearchtree.png]]

### Definitions 
A **tree** consists of: 
- A set of nodes
- A set of edges that connect those nodes
	- Constraint: there is exactly one path between any two nodes

In a **rooted** tree, we call one node the root.
- Binary tree: 0, 1, or 2 children 
- Not binary tree: more than 2 children for one parent

A BST is a rooted binary tree with the **BST property**.

**A BST Property**: 
- Every key in the left subtree is less than X's key
- Every key in the right subtree is greater than X's key 

![[bstrules.png]]

### BST Operations: Search

If searchKey equals T.key, return.
- If searchKey < T.key, search T.left
- If searchKey > T.key, search T.right 

```java 
// NOT A REAL JAVA CODE
static BST find(BST T, Key sk) {
	if (T == null) {
		return null;
	} 
	if (sk.equals(T.key)) {
		return T;
	} else if (sk < T.key) {
		return find(T.left, sk);
	} else {
		return find(T.right, sk);
	}
}
```

The runtime to complete a search on a "bushy" BST in the worst case is Theta(log N). 
Height of the tree is ~log2(N).

### BST Operations: Insert
![[insert.png]]

### BST Operations: Deletions
3 cases: 
1. Deleting a node with no children (simple)
2. Deleting a node with 1 children (move the node's parent's pointer to the node's child)
	- an F's child will be definitely larger that D(F's parent): E and G come later than D
3. Deleting a node with 2 children:
	- Must be > than everything in the left subtree
	- Must be < than everything in the right subtree 

> An important idea in algorithm design: be lazy

![[deletingroot.png]]

the predecessor of the deleted item = the largest item that is smaller
the successor of the deleted item = the smallest item that is larger

> Neither predecessor nor successor will have more than 1 children. 

![[before.png]]
![[after.png]]


### Sets vs. Maps 
Can think of the BST below as representing a Set: 
- {mo, no, sumomo, uchi, momo} 
- the picture below without values would be just a Set
![[bstrepresentationset.png]]


Two ways to implement a Set (or Map): ArraySet and using a BST
- ArraySet: Theta(N) operations in the worst case
- BST: Theta(log N) operations if tree is balanced

### BST Implementation Tips
- For each public method, e.g. put(K key, V value), create a private recursive method, e.g. put (K key, V value, N node) 
- When inserting, always set left/right pointers, even if nothing is actually changing 
- Avoid "arms length base cases". Don't check if left or right is null!





