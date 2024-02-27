## Goal: Building a List

```java
import java.util.List;
import java.util.LinkedList;

List<String> L = new LinkedList<>();
L.add("a"); 
L.add("b"); 
```

- Recursion will allow us to build infinite lists 

### The Walrus Mystery 
```java 
Walrus a = new Walrus(1000, 8.3)' 
Walrus b; 
b = a; 
b.weight = 5; 
System.out.println(a); 
System.out.println(b);
```
Will the change to b affect a?  - Yes 

```java
int x = 5; 
int y; 
y = x; 
x = 2;
```
In this case, no. 

### Bits
Your computer stores information in "memory"
- Information is stored in memory as a sequence of ones and zeros 
	- Example: 72 stored as 01001000
- Each Java type has a different way to interpret the bits: 
	- 8 primitive ones: byte, short, int, long, float, double, boolean, chat

### Declaring a Variable (Simplified)
When you declare a variable of a certain type in Java: 
- Your computer sets aside exactly enough bits to hold a thing of that type. 
	- Example: declaring an int sets aside a "box" of 32 bits 
- Java creates an internal table that maps each variable name to a location 
- Java does NOT write anything into the reserved boxes
	- For safety, Java will not let access a variable that is uninitialized (there already bits there, but the variable's value was not set)

### The Golden Rule of Equals 
- y = x copies all the bits from x into y

### Reference Types
Everything else besides the primitive types.

When we instantiate an Object (Dog, Walrus, Planet, etc.)
- Java first allocates a box of bits for each instance variable of the class and fills them with a default value (e.g 0, null)
- The constructor then usually fills every such box with some other value. 

When we declare a variable of any reference type: 
- Java allocates exactly a box of size 64 bits, no matter what type of object. 
- These bits can be either set to: 
	- Null (all zeros)
	- The 64 bits "address" of a specific instance of that class (returned by new)
	- The 'Walrus' instance is 96 bits, but the address that we store is 64 bits.

![[instantiation and declaration.png]]

### Reference Types Obey the Golden Rule of Equals
Just as primitive types, the equals sign copies the bits

- In terms of our visual metaphor, we "copy" the arrow by making the arrow in the b box point at the same instance as a.

```java
Walrus a; 
a = new Walrus(1000, 8.3);
Walrus b; 
b = a;
```

![[reference types golden rule of equals.png]]

### Parameter Passing
Passing parameters obeys the same rule: simply copy the bits to the new scope.

- b = a copies the bits from a into b
- passing parameters copies the bits


![[arrays.png]]

- If we were to reassign a to something else, we'd never be able to get the original Object back! 


## IntList and Linked Data Structures

```java 
// the recursive solution for the size
public int size() {
	if (rest == null) {
		return 1; 
	}
	return 1 + this.rest.size();
}

public int iterativeSize() {
	IntList p = this; 
	int totalSize = 0; 
	while (p != null) {
		totalSize += 1;
		p = p.rest; 
	}
}

public int get(int i) {
	if (i == 0) {
		return this.first; 
	}
	return this.rest.get(i - 1); 
}
```

