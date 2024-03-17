### The problem with 2-3, 3-4 Trees
--> Real pain to implement, and suffer from performance problems.

Issues include: 
- maintaining different node types 
- interconversion of nodes between 2-nodes and 3-nodes
- walking up the tree to split nodes

"Beautiful algorithms are, unfortunately, not always the most useful" - Knuth

## Tree Rotation

Can also be thought as merging GP, then sending G down and left. 
![[firstrotation.png]]
When P becomes the parent of G, G loses the right node, and P's left node is no longer k but G. That's why we assign k as the right node of G. 

Some rotations are undefined.![[undefinedrotation.png]]

#### Why use rotation? 
- can shorten (or lengthen) a tree
- preserves search tree property 



## 2-3 Tree as a BST 

Current Search Trees: 
- Binary search trees: can balance using rotation, but we have no algorithm for doing so (yet)
- 2-3 trees: balanced by construction, i.e. no rotations required

**Our goal**: build a BST that is structurally identical to 2-3 tree

**Possibility 1**: Create dummy "glue" nodes.
- result is inelegant 
- wasted link 
- code will be ugly 

**Possibility 2:** create "glue links" with the smaller item **off to the left**.![[possibility2.png]]

A BST with left glue links that represents a 2-3 tree is often called a "Left Leaning Red Black Binary Search Tree" or LLRB. 
- LLRBs are normal BSTs! 
- There is a 1-1 correspondence between LLRB and an equivalent 2-3 tree 
- The red is just a convenient fiction. Red links don't "do" anything special. 

### Valid / Invalid LLRBs
![[validorinvalid.png]]

### LLRB Properties
![[llrb height.png]]

- No node has two red links (otherwise it'd be analogous to a 4 node, which are disallowed in 2-3 trees)
- Every path from root to null has same number of black links (because 2-3 trees have the same number of links to every leaf). LLBs are therefore balanced.

> Because 2-3 trees have logarithmic height, and the corresponding LLRB has height that is never more than ~2 times the 2-3 tree height, LLRBs also have logarithmic height!



## LLRB Construction 

Where do LLRBs come from? 
- Would not make sense to build a 2-3 tree, then convert. Even more complex. 
- Instead, it turns out we implement an LLRB insert as follows: 
	- Insert as usual into a BST
	- Use zero or more rotations to maintain 1-1 mapping

### The 1-1 Mapping 
There exists a 1-1 mapping between: 
- 2-3 tree 
- LLRB

> Implementation of an LLRB is based on maintaining this 1-1 correspondence. 
- When performing LLRB operations, pretend like you're a 2-3 tree
- Preservation of the correspondence will involve tree rotations 



### Design Tasks 

#### #1: Insertion Color
> We should use red link when inserting. In 2-3 trees new values are ALWAYS added to a leaf node (at first)

#### #2: Insertion on the Right
LLRBs are left-leaning, meaning the smaller item goes to the left. In this example, 'E' didn't go to the left. We solve it by rotation.

![[insertionontheright.png]]


#### New Rule: Representation of Temporary 4-Nodes
![[newrule.png]]
#### Design Task #3: Double Insertion on the Left
![[4designproblem.png]]


#### Design Task #4: Splitting Temporary 4-Nodes
![[designtask4.png]]


#### ... and That's It! 
- When inserting: use a red link 
- If there is a *right-leaning "3-node",* we have a Left Leaning Violation
	- **Rotate left** the appropriate node to fix 
- If there are two consecutive left links, we have an incorrect 4 Node Violation
	- **Rotate right** the appropriate node to fix
- If there are any nodes with two red children, we have a Temporary 4 Node
	- Color flip the node to emulate the split operation

One last detail: Cascading operations
- It is possible that a rotation or flip operation will cause an additional violation that needs fixing 


### Cascading Balance
![[cascadingbalance.png]]
Should not have a red link to the right of B. 

**Solution:** 
![[cascading.png]]

### Optional Exercise 
Rules: 
1. Right red link --> rotate left (? move the parent up)
2. Two consecutive left links --> rotate right (? move the the middle node up)
3. Red left and red right --> color flip 


## LLRB Runtime and Implementation

- LLRB tree has height O(log N)
- Contains is trivially O(log N)
- Insert is O(log N)
	- O(log N) to add the new node
	- O(log N) rotation and color flip operations per insert 

```java 
private Node put(Node h, Key key, Value val) {
	if (h == null) {
		return new Node(key, val, RED); 
	}

	int cmp = key.compareTo(h.key);
	if (cmp < 0) {
		h.left = put(h.left, key, val);
	} else if (cmp > 0) {
		h.right = put(h.right, key, val);
	} else {
		h.val = val; 
	}

	if (isRed(h.right) && !isRed(h.left)) {
		h = rotateLeft(h);
	} 
	if (isRed(h.left) && isRed(h.left.left)) {
		h = rotateRight(h);
	} 
	if (isRed(h.left) && isRed(h.right)) {
		flipColors(h);
	}
}
```

Java's TreeMap is a red-black-tree (not left leaning)