Our search tree based sets require items to be comparable. Any way we could get around this and improve our `log N` runtime?

**Two functions of a set**: 
- add 
	- assume we are not adding duplicates because we check contains first 
- contains 

1st analogy - a paper and a wall. Fast add, long contains.

Checking the last number in your SnackPass order: 
![[boba.png]]

**Problems of this solution:**
1. Waste of space (for empty slots in a bin / section)
2. What if the set gets so big that even the bins are 1000 in size?
3. What happens if the numbers aren't evenly distributed or random (e.g most end in 0)?
4. What if we want to deal with things that aren't numbers?

Main problem - sections are too big. 

### How to minimize wasted space? 
Instead of assuming the same amount of wall space per section, dynamically increase the size of each section as items get added there.

Easiest solution to implement is to use Linked Lists.
- Still one unit of wasted space might exist (e.g. is one of the sections have no items), but much more better waste management

Let N = number of items in all bins, M = number of bins 
--> contains runs in Θ(M / N) time. 

- **Solution**: have M grow with N so that each bucket has on average a constant number of elements
	- When we increase M, we'll have to reassign every number to a new box, which will take Θ(N) time during add operation
	- Our goal is to have Θ(1) amortized runtime, and we've seen from ArrayLists that we can get that as long as we do Θ(N) steps rarely enough
	- Therefore, M should double every time (squaring would result in too much of unused space again)
- Needs a way to categorize numbers into M groups for arbitrary M: "last digit" only works with M = 10 
	- --> **modulus (remainder of division)** is the most natural and best reduction function. 

Resizing example: 
![[resizingexample.png]]

This data structure might be called a DynamicArrayOfListsSet.

If we have N items that are evenly distributed, length of each list is ~N/M.
- N/M is constant asymptotically
- So operations are constant on average 


### How to work with strings?
One idea: use the letter in the alphabet of the first letter as the list number. 
- after resizing will use the first two letters: "aa", "ab", etc.

What are some issues with the approach? 
- Where to put short strings (e.g "a") after resize? (can probably fix)
- It feels wrong for Strings to force our Set to resize to multiples of 26
	- Are we going to have a unique resize for every type of object??

**Silly solution:** force every object to know how it converts to Int.

**How to convert 'cat' into a number?**
--> use a 26-base number system (unique for every lowercase word)

**ASCII is doing exactly this for every symbol!**

### ASCII on steroids = Unicode 
New problem! (Who might have expected...)

- The Ints get too large and in Java they are limited
- Overflow = going over the limit, the number will start back at the smallest integer (i.e negative billion)

The official term for the number we're computing is "hash code".

Because the range of our hashCode is finite, it is impossible to pursue unique factorizations for each string. 

Instead of base 40, 959 or something larger, Java uses 31.


### Hash Table
We have just created a **hash table.**

![[hashtable.png]]

Hash tables are the most popular implementation for sets and maps.
- Great performance 
- Don't require compatable
- Implementations are relatively simple 
- Python dictionaries are just hash tables in disguise

All objects in Java must implement a .hashCode 
- default implementation is a memory address (kind of random, but the same on one machine)

```java 
// Java's actual hashCode function for strings
public int hashCode(String s) {
	int intRep = 0;
	for (int i = 0; i < s.length(); i += 1) {
		intRep = intRep * 31;
		intRep = intRep + s.chatAt(i);
	}
	return intRep;
}
```

Use .floorMod instead of modular (allows -1 to go in the end of the range)


### The runtime and the Summary
With no resizing M, it is Θ(N). With resizing - O(1)

Even distribution is critical for good for hash table performance. 

![[hashsummary.png]]










