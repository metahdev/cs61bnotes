### Casting and Dynamic Method Selection (DMS)

Compile-time error is guaranteed if it is obvious based on the code. 

```java
(List) new Dog(); // compile-time error
(Dog) ((Animal) new Cat()); // run-time error

Animal x = new Dog();
(Dog) x; // allowed 

Animal y = new Animal();
(Dog) y; // not allowed (run-time error)
```

Interesting fact: after compiling once, you can run the same code repeatedly without going through the checks above, so it's faster




