A data structure that lets you interact with the smallest / largest item. 

Naive approach: sort the existing array and return the first element. 
- potentially uses a huge amount of memory Theta(N) 

**Goal**: do this in Theta(M) memory using a MinPQ

One solution: once the size > M, remove the smallest item (if we need the biggest M eventually) —> leads smaller size

What data set should we use for MinPQ?

## Heaps 
Binary, complete, and min-heap. 

![[Introducing the Heap.jpeg]]

### Heap Operations 

**Insert 3:**
- add to the end of the heap temporarily 
- swim up the hierarchy to your rightful place...
![[swimming.png]]
3 used to be at the most bottom right 5. 


**Delete min:**
- Swap the last item in the heap into the root 
	- ruined the min-heap property! 
- sink its way down the hierarchy, yielding to the most qualified folks


**PQ Operations:**
- getSmallest() - return the item in the root node 
- add(x) - place the new employee in the last position, and promote as high as possible 
- removeSmallest() - assassinate the president (of the company), promote the rightmost person in the company to president. Then demote repeatedly, always taking the 'better' successor. 

How do we do it in Java? 


### Tree Representations 

1A. Recursive implementation (having a Node class with left, middle, and right links)
	- BSTMap used this approach 
1B. Create an array of children
	- code a little awkward and performance not too good
1C. Sibling tree (one link to the first child that has a right link to its sibling)
	- a horizontal linked list of siblings 
2. Store keys in array. Store parentIDs in an array
	- Similar to DisjointSets
3. Array of Keys

from 2 to 3: 
![[approachDisjointSets.png]]

As you can see, in a complete tree the parents list is redundant. ![[onedimensionaltree.png]]

A Deep Look: 
```java 
public class Tree3<Key> {
	Key[] keys; 
	...

	public void swim(int k) {
		if (keys[parent(k)] > keys[k]) {
			swap(k, parent(k));
			swim(parent(k));
		}
	}

	public int parent(int k) {
		return (k - 1) / 2;
	}
}
```

> **Approach 3B: Leaving One Empty Spot**
- Same as 3, but leave index 0 empty
- Makes computation of children/parents "nicer"
	- leftChild(k) = k * 2;
	- rightChild(k) = k * 2 + 1;
	- parent(k) = k / 2;


### Heap Implementation of a Priority Queue
- Why "priority queue"? Can think of position in tree as its "priority"
	- the root is the highest priority
- Heap is log N time AMORTIZED (some resized, but no big deal)
- BST can have constant getSmallest if you keep a pointer to smallest
- Heaps handle duplicate priorities much more naturally than BSTs
- Array based heaps take less memory (very roughly about 1/3rd the memory of representing a tree with approach 1a)

# Summary
![[theholydatastructuresgrail.png]]

*ChainingHT and Linear Probing HT are just Hash Tables*

