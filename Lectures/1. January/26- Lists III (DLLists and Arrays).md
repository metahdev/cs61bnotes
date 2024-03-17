![[improvement.png]]

### Problem: Adding the Last is Slower Than Adding First
Is having the last pointer enough? - No, remove would be slow

- In order to delete from the end of the list fast, we have to add backwards links from every node. 
- This yield a "doubly linked list" or DLList, as opposed to our earlier "singly linked list" or SLList

However, Last is not an invariant which is a bad design.

![[naive dllist problem.png]]

One solution: have two sentinels. 
 ![[better topology.png]]

When we convert our SLList to Generic: 
``` java
SLList <String> s1 = new SLList<>("bone");
```

When declaring or instantiating your data structure, use the reference type.
 - int: Integer
 - double: Double 
 - char: Character
 - boolean: Boolean 
 - long: Long

## Our Long Term Goal: The AList

**Arrays** are a special kind of object which consists of a **numbered sequence** of memory boxes. 
- To get ith item of array A, use A[i]
- Unlike **class** instances which have named memory boxes (properties)

Arrays consists of: 
- A fixed integer length (cannot change!)
- A sequence of N memory boxes where N= length, such that: 
	- All of the boxes hold the same type of value (and have same # of bits)
	- The boxes are numbered 0 through length - 1

Like instances of classes:
- You get one reference when its created.
- If you reassign all variables containing that reference, you can never get the array back.

Unlike classes, arrays do not have methods.

Three valid notations: 
```java 
y = new int[3]; // 32 * 3 = 96 bits total
x = new int[]{1, 2, 3, 4, 5}; 
int[] w = {9, 10, 11, 12, 13}; // can omit the new if you are also declaring 
```

Two ways to copy arrays: 
- Item by item using a loop
- Using arraycopy. Takes 5 parameters: 
	- Source array
	- Start position in source 
	- Target array 
	- Start position in target
	- Number to copy

### 2D Arrays
```java
int[][] matrix;
matrix = new int[4][] // creates an array of null references to other arrays
matrix = new int[4][4] // creates 5 arrays: 1 that contains references to other arrays, 4 arrays themselves
```


Class member variable names CANNOT be computed and used at runtime. 