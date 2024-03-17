![[ntable.png]]

![[example.png]]
Answer: C

![[graph.png]]

>**There is no magic shortcut for asymptotic analysis problems**.

![[expected.png]]

Strategies: 
- find exact sum 
- write out examples 
- draw pictures

in some cases, can use definite integrals as a shortcut.

### Amortized Analysis

Dividing the code into several functions does not affect the runtime. 

```java 
public void addMany(int n) {
	for (int i = 0; i < n; i++) {
		// saying i *= 2 would not change the order of growth as we know from the printParty before (Theta N)
		addLast(1); 
	}
}

public void addLast(int value) {
	if (this.length == arr.length) {
		resize(this.length * 2);
	} // happens every time length is 2^k
	// addLast code takes 1 unis of work
}

public void resize(int i) {
	// resizing takes i units of work 
}
```

Now we can prove why geometric resizing is better than arithmetic with asymptotics: 
![[addLast comparisons.png]]

This is known **Amortized Runtime**: 
- Any single operation may take longer, but if we use it over many operations, we're guaranteed to have a better average performance 
- So amortized runtime gives a better estimate of how much time it takes to use something in practice 
- Disjoint sets also used amortized runtime; WQU with path compression still has Theta(log(N)) runtime in the worst case, but Theta(a(n)) amortized runtime. 

### Tree Recursion 

The order of growth of runtime of a tree is 2^N (every node is doubled). 
![[finalterm.png]]

> Considering specific examples help. The final term is 4 when N = 3 --> 2^N-1 (answer D)

C(N) = 2^N - 1 because

1 + 2 + 4 + 8 + ... + Q = 2Q - 1 (Sum of the First Powers of 2 from the printParty)
since Q = 2^N - 1 ---> C(N) = 2Q - 1 = 2^N - 1


### Binary Search

Intuitively, the order of growth is log2N since the array is cut in half continuously.

In practice, logarithmic time algorithms have almost constant runtimes.

### Handy Big Theta Properties 
![[big theta properties.png]]

## Sorting
### Selection Sort
1. Find the smallest unfixed item, move it to the front, and 'fix' it
2. Sort the remaining unfixed items using selection sort

Runtime of selection sort is Theta(N^2): 2 + 3 + 4 + 5 + ... + N.
If N = 64, arbitrary unit of time (AU) = 64^2

### Merging
**Array Merging:** given two arrays, the merge operation combines them into a single sorted array by successively copying the smallest element from the two arrays into the target array. 
![[arraymerging.png]]
N = 9 

Merging can give us an improvement over vanilla selection sort: 
- Selection sort the left half: Theta(N^2)
- Selection sort the right half: Theta(N^2)
- Merge the results: Theta(N)
![[selectionsort.png]]

Can do even better by adding a second layer of merges.
![[twomergelayers.png]]

As we go down, we end up with arrays of size 1 that do not require selection sort. 

### Mergesort
- If array is of size 1, return
- Mergesort the left half: Theta(?)
- Mergesort the right half: Theta(?)
- Merge the results: Theta(N)

![[mergesortruntime.png]]

### Using Sorting as a Tool 
![[dup.png]]

Combining sorting (Theta(NlogN)) with dup2 (Theta(N)) is better than using dup1  (Theta(N^2))

### Summary
- No magic shortcuts since theoretical analysis requires careful thought 
- But for this course, know that 
	- 1 + 2 + 3 + ... + N is Theta(N^2)
	- 1 + 2 + 4 + ... + N is Theta(2N - 1)
- One of the highest skill ceilings of all topics in the course 

Different solutions to the same problem may have different runtimes
- N^2 vs N log N is an enormous difference
- N log N to N is nice, but not a radical change

Once you prove runtime for one problem, you may be able to use it in other problems to speed things up!

*Theta = Θ\**
