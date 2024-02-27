```java
// The new and improved IntList - SLList
public class SLList {

	// making it static because it does not access SLList object's properties 
	private static class IntNode {
		public int item; 
		public IntNode next; 

		public IntNode(int i, IntNode n) {
			item = i; 
			next = n;
		}
	}
	private IntNode first; // we make it private so that the user can't manipulate with the raw data

	public SLList(int x) {
		first = new IntNode(x, null); 
	}

	public static void main(String[] args) {
		SLList L = new SLList(10); 
		L.addFirst(10);
		L.addFirst(5);
	}

	public void addFirst() {
		first = new IntNode(x, first); 
	}

	public int getFirst() {
		return first.item;
	}

	public void addLast(int x) {
		if (first == null) {
			first = new IntNode(x, null);
			return;  
		}
		// - ugly code that is solved by having sentinel (a node before the first node)

		IntNode p = first; 

		while (p.next != null) {
			p = p.next;
		}
		p.next = new IntNode(x, null); 
	}

	private static int size(IntNode p) {
		// the language of Gods
		if (p.next == null) {
			return 1; 
		}
		return 1 + size(p.next);
	}

	public int size() {
		// the language of the middle man, needed to implement recursively
		return size(first); 
	}
}
```

![[intlist vs sllist.png]]

```java

public class SLList {

	private static class IntNode {
		public int item; 
		public IntNode next; 

		public IntNode(int i, IntNode n) {
			item = i; 
			next = n;
		}
	}
	private IntNode sentinel;
	private int size; 

	public SLList() {
		sentinel = new IntNode(63, null); 
		size = 0;
	}

	public SLList(int x) {
		sentinel = new IntNode(63, null);
		sentinel.next = new IntNode(x, null); 
		size = 1;
	}

	public static void main(String[] args) {
		SLList L = new SLList(10); 
		L.addFirst(10);
		L.addFirst(5);
	}

	public void addFirst() {
		sentinel.next = new IntNode(x, sentinel.next); 
		size += 1; 
	}

	public int getFirst() {
		return sentinel.next.item;
	}

	public void addLast(int x) {
		size += 1; 

		IntNode p = sentinel;
		while (p.next != null) {
			p = p.next; 
		}

		p.next = new IntNode(x, null); 
	}

	public int size() {
		return size; 
	}
}
```

## Invariants 
An invariant is a condition that is guaranteed to be true during code execution. 

An SLList with a sentinel node has at least the following invariants: 
- The sentinel reference always points to a sentinel node
- The first node (if exists), is always at sentinel.next
- The size variable is always the total number of items that have been added

Invariants make it easier to reason about code: 
- Can assume they are true to simplify code 
- Must ensure that methods preserve invariants

