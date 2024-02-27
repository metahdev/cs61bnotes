If you want one class to be a hyponym of another class, you use extends.

```java 
public class RotatingSLList<Item> extends SLList <Item> {
	// rotating list to the right
	public void rotateRight() {
		Item x = removeLast(); 
		addFirst(x); 
	}	
}
```

Because of extends, RotatingSLList inherits all members of SLList:
- All instance and static variables.
- All methods.
- All nested classes.
Constructors are not inherited.

We can `@Override` methods in Extends too. 
	The problem: `private` in Java means so private, that even your subclasses can't access it.
	The solution: `super.method();`
```java
@Override 
public Item removeLast() {
	Item x = super.removeLast(); 
	deletedItems.addLast(x);
	return x;
}
```
Note: Java disallows super.super.

- You must use "implements" if the hypernym is an interface and the hyponym is a class 
- You must use "extends" in all other cases

### Constructor Behavior is Slightly Weird

Constructors are not inherited. However, the rules of Java say that all constructors must start with a call to one of the super class's constructors. 

- Idea: If every VengefulSLList is-an SLList, every VengefulSLList must be set up like an SLList.
- You can explicitly call the constructor with the keyword `super();`
- If you don’t explicitly call the superclass's constructor, **Java will automatically call the super no-argument constructor**
	- If it didn’t call SLList constructor, sentinel would be null. Very bad.

**All classes in Java are the descendants of the Object class**

![[abomination.png]]

## Encapsulation

When building large programs, our enemy is complexity. 

Some tools for managing complexity: 
- Hierarchical abstractions 
	- Create layers of abstraction, with clear abstraction barriers
- "Design for change"
	- Organize program around objects
	- Let objects decide how things are done (override)
	- Hide information others don't need

Managing complexity supremely important for large projects (e.g. project 2)

**Module:** A set of methods that work together as a whole to perform some task or set of related tasks. 

A module is said to be **encapsulated** if its implementation is *completely hidden*, and it can be accessed only through a documented interface. 

### Implementation Inheritance Breaks Encapsulation 

![[theloop.png]]
Code above is stuck in an infinite loop because the dynamic type of `barkMany(1)` in the superclass calls the implementation of the subclass. 

### Compile-Time Type Checking 

Compiler allows method calls based on compile-time (static) type of variable. 
- x is VSlist run-time but Slist compile-time (VSlist extends Slist)
- x's methods present in Slist will be called based on the latest implementation in VSlist
- However compiler cannot call unique VSlist methods from x since its compile type is SList
*my question in the previous lecture notes

The same is true for assigning a Subclass instance to Superclass declaration. 
	Image below as an example. 
![[compiletypechecking.png]]

You can assign a superclass declaration to subclass instantiation, but not the other way around (subclass is always a superclass, but superclass is not always a subclass)
![[compiletypes.png]]

Methods also have compile-time type equal to their declared type. 

### Casting

Java has a special syntax for forcing the compile-time type of any expression. 

![[casting.png]]

**Casting is powerful but dangerous!**

## Higher Order Functions 

**Higher Order Function:** A function that treats another function as data (e.g. takes a function as an input). 

We can use interfaces to create them in Java.

```java 
public interface IntUnaryFunction {
	int apply(int x); // public is reduntant
}

public class Tenx implements IntUnaryFunction {
	public int apply(int x) {
		return 10 * x
	}
}

public class HofDemo {
	public static int do_twice(IntUnaryFunction f, int x) {
		return f.apply(f.apply(x));
	}

	public static void main(String[] args) {
		IntUnaryfunction tenX = new TenX(); 
		System.void.println(do_twice(tenx, 2));
	}
}
```

Note: In Java 8, new types were introduces: now can hold references to methods. 

- For overridden methods the actual method invoked is based on dynamic type of invoking expression
	- Does not apply to overloaded methods! 

