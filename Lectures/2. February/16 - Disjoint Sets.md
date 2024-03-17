**Goal**: deriving the "Disjoint Sets" data structure for solving the "Dynamic Connectivity" problem. We will see: 
- How a data structure design can evolve from basic to sophisticated 
- How our choice of underlying abstraction can affect asymptotic runtime (using out formal Big-Theta notation) and code complexity

**DS has two operations**: 
- connect(x, y) 
- isConnected(x, y)

### The Disjoints Sets implementation

Two simplifications: 
- integer elements
- fixed number of elements 

```java 
public interface DisjointSets { 
	void connect(int p, int q);
	boolean isConnected(int p, int q);
}
```

**The naive approach**: 
1. Keep track of the lines 
2. Iterate through them to find if the elements are connected

**A better approach: Connected Components**
![[a better approach.png]]

**Storing the sets in a list is not the best idea:** 
![[listsets.png]]

"Choosing the basic blocks for further abstraction building is extremely important."

**Idea #2: list of integers where ith entry gives set number (a.k.a. "id") of item i**
![[idea2.png]]

The implementation: 
![[quickfindds.png]]

QuickFindDS is too slow for practical use: connecting two items takes N time. 
- Instead, let's try something more radical

### Quick Union
We will still represent everything as connected components, and we will still represent connected components as a list of integers. However, values will be chosen so that connect is fast. 

![[ageniusmathuniverse.png]]

Potential drawback: 
- long isConnected
- worst case runtime of connect is Theta(N) if the tree gets too tall

```java
public class QuickUnionDS implements DisjointSets {
	private int[] parent;
	
	public QuickUnionDS(int N) {
		parent = new int[N];
		for (int i = 0; i < N; i++) {
			parent[i] = -1;
		}
	}

	// For N items, this means a worst case runtime is Theta(N)
	private int find(int p) {
		int r = p;
		while (parent[r] >= 0) {
			r = parent[r];
		}
		return r; 
	}

	public boolean isConnected(int p, int q) {
		return find(p) == find(q);
	}

	public void connect(int p, int q) {
		int i = find(p); 
		int j = find(q);
		parent[i] = j;
	}
}
```

### Weighted Quick Union 
A modification of QuickUnionDS that accounts for tree size.

Why not 'heighted' quick union: asymptotic difference is not present, both are log(N). Resulting code would be much more complicated for no reason. 

**Key point:** a good data structure unlocks solutions to problems that could otherwise not be solved! 

### Path Compression 

![[pathcompression.png]]

By compressing the tree with each union and isConnected call, we keep the tree nice and short.
- As number of nodes N grows, our tree tends to get taller
- As number of operations M grows, out tree tends to get shorter
	- For enough operations tree height will shrink to 1

Average run-time: lg* N (<5 for any realistic input)

You can provide an even tighter bound, showing that each operation takes on average α(N) time. 
- α is the inverse Ackermann function.
- See “Efficiency of a Good But Not Linear Set Union Algorithm" written by Bob Tarjan while at UC Berkeley in 1975.






