## Interface
1. Overloading: multiple methods with same name, but different parameters
2. Hypernyms - dog, hyponym - husky 
3. Interface: a specification of what to do, not how to do it (`implements`)
4. `@Override` annotation is not important for compilation, rather for the programmer
5. Subclasses must override all of the interface's methods

![[interfaceandclass.png]]

My question: Can you access methods unique to SLList through someList? 
-No, unless you cast it. 

7. `default` keyword allows us to create implementation in our interfaces
 ![[alistandsllist.png]]
SLList has incremental implementation of get, that is why one implementation for both subclasses is often not optimal.
## Dynamic Method Selection

Once a default implementation is overridden in the subclass, we use the overridden implementation even if the variable's type is Interface.  ![[override.png]]

 - Static Type: the type specified at declaration. Never changes! (List61B above)
-  Dynamic Type: the type specified at instantiation (e.g when using new). Equal to the type of the object being pointed at. 

 Dynamic method selection: 
	- compile-time type variable X
	- same variable with run-time type Y
	If Y overrides the method, Y's method is used instead. 

- Interface Inheritance: allows you to generalize code in a powerful, simple way. 
- Implementation Inheritance (how): allows code-reuse
- Important: in both cases, we specify "is-a" relationship, not "has-a"
	- Good: Dog -> Animal, SLList -> CS61BList
	- Bad: Cat -> Claw, Set -> SLList

The Dangers of Implementation Inheritance: 
	- Makes it harder to keep track of where something was actually
	- Rules for resolving conflicts can be arcane
	- Encourages overly complex code: common "has-a" vs. "is-a"
	- Break encapsulation\