### Tree Height, Big O vs Worst Case

![[bushyandspindly.png]]

O(N) is "less than or equal"
![[statements.png]]

Statement A is more informative than statement B and C. 

Analogy: 
![[hotel.png]]

BST height is all of these: 
- O(N)
- Theta(log N) in the best case ("bushy")
- Theta(N) in the worst case ("spindly")
- O(N^2)

The middle two statements are more informative.
- Big O is NOT mathematically the same thing as "worst case"
	- e.g. BST heights are O(N^2), but are not quadratic in the worst case
	- ... but Big O is often used as shorthand for "worst case"


#### The Usefulness of Big O

Big O still a useful idea: 
- Allows us to make simple blanket statements, e.g. can just say "binary search is O(log N)" instead of "binary search is Theta(log N) in the worst case"
- Sometimes don't know the exact runtime, so use O give an upper bound
	- Example: Runtime for finding shortest route that goes to all world cities is O(2^N). There might be a faster way, but nobody knows yet.
- Easier to write proofs for Big O than Big Thera, e.g. finding runtime of mergesort, you can round up the number of items to the next power of 2. 


## Back to Trees: Height and Depth

Height and average depth are important properties of BSTs.
- The "depth" of a node is how far it is from the root
- The "height" of a tree is the depth of its deepest leaf 
- The "average height" of a tree is the average depth of a tree's nodes

![[height and depth.png]]

The order we add elements determines the hierarchy of the tree. 
![[examples.png]]

**Nice Property:** trees built from random inserts have Theta(log N) average depth and height. 
- In other words: random trees are bushy, not spindly. 
- The same is true for random deletion

**Bad news:** we can't always insert out items in a random order. 




## B-Trees
### Avoiding Imbalance

Overstuffed trees are a logically consistent but very weird data structure.
![[avoidimbalance.png]]

How about moving items up?
![[movingup.png]]

**The problem now:** 16 being on the right of 17. Solution: 
- Pull item out of full node splitting it into left and right 
- Parent node now has tree children! 
![[btreeintro.png]]


### Chain Reaction Splitting

What happens if the tree gets too large? 
![[fattree.png]]

Observation: splitting-trees have perfect balance
- if we split the root, every node gets pushed down by exactly one level
- if we split a leaf node or internal node, the height doesn't change

All operations have a guaranteed O(log N) time. More details soon. 

### Terminology
Splitting-Trees are actually called **B-Trees**.

- B-trees of order L=3 (like we just used) are also called a 2-3-4 tree or a 2-4 tree. 
	- "2-3-4" refers to the number of children that a node can have
	- max 3 items per node, and max 4 non-null children per node
- B-trees of order L=2 are also called a 2-3 tree.
	- max 2 items per node, and max 3 non-null children per node

B-Trees are most popular in two specific contexts: 
- Small L(2 or 3)
	- Used as a conceptually simple balanced search tree
- L is very large 
	- Used in practice for databases and filesystems


### B-Tree Bushiness Invariants
No matter the insertion order resulting B-Tree is always bushy!
- May vary in height however

Because of the way B-Trees are constructed (from bottom to top): 
- All leaves must be the same distance from the source
- A non-leaf node with k items must have exactly k+1 children
![[impossible.png]]


### Runtime Analysis

Height of a B-Tree with Limit L:
![[limit l.png]]

If H = Theta(log N), overall runtime is O(L log N). 
Since L is constant, runtime is therefore O(log N).


### Summary
BSTs have best case height Theta(log N), and worst case height Theta(N). 
- Big O is not the same thing (technically) as worst case!

B-Trees are a modification of the binary search tree that avoids Theta(N) worst case.
- Nodes may contain between 1 and L items.
- contains works almost exactly like a normal BST.
- add works by adding items to existing leaf nodes.
	- If nodes are too full, they split.
-  Resulting tree has perfect balance. Runtime for operations is O(log N).
- Have not discussed deletion. See extra slides if you're curious.
- Have not discussed how splitting works if L > 3 (see some other class).
- B-trees are more complex, but they can efficiently handle ANY insertion order.

*Theta = Θ\**