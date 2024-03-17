HashCode comparison:

- No spread: returning 0
- Bad spread: returning sum of the digits
- Good spread: returning num 

The elements in a hash table are distributed by their hash code, therefore a good hash code has a good spread. The default hashCode - memory address - has a good spread. 

### Why bother with custom hash function when a memory address hashCode works perfectly fine?

Even if we write a custom equals by the number, contains(ColoredNumber(12)) will return a random answer because it will check a category according to a new object’s memory address, not its number value. 
- It's necessary to have consistency between equals and hashCode for basic operations to function 
- Inconsistency might lead to duplicates since the item will be checked for `contains` in the wrong bucket

> Basic rule: if two objects are equal, they’d better have the same hashCode so the hash table can find it.


## Immutable vs. Mutable 

![[Immutable Data Types.jpeg]]

### Clarification from ChatGPT:
  
In Java, the `String` class is considered immutable because once a `String` object is created, its state cannot be changed. This means you cannot modify the contents of a `String` object after it has been created.

When you perform operations like concatenation or appending to a `String`, what happens under the hood is that a new `String` object is created to hold the result of the operation, while the original `String` remains unchanged. For example:

```java 
String str1 = "Hello"; 
String str1 += " World";  // concatenation creates a new instance that is now 
                          // referenced by the str1 variable
```

In this example, `str1` remains "Hello" and a new `String` object containing "Hello World" is created and assigned to `str2`.


### Examples: 

In this case, although the rocks in the RocksBox is a `final` variable that can not be instantiated again, it is still mutable by accessing and changing elements through an index. 
![[immutable.jpeg]]

Now, if we change it to private, we still can mutate the rocks through another variable that holds the reference to the same object. 
![[Which of the Classes Below Are Immutable 1.jpeg]]

To ensure that does not happen, we need to copy a potentially mutable data structures in our constructors. 
![[How Would We Make SecretRocksBox Immutable.jpeg]]

  
**Immutability**:
\+ less to think about 
\+ avoid bugs and makes debugging easier 
- Analogy: immutable classes have some buttons you can press/ windows you can look inside. 
- Results are ALWAYS the same, no matter what

\- Must create a new object anytime anything changes 
- Example: string concatenation is slow

  
### Mutable Hash Table Keys
Imagine you have a hash table of lists. 

1. You add a list [1, 7] with hash code 902
2. It goes to category 2 
3. You add an item to that list and make it [1, 7, 9] 
4. You check contains ([1, 7, 9]) and get False 

This happens because [1, 7, 9]’s hashCode is 17805 so the hash table checks in the wrong section! (5 with modular)

> Bottom line: never mutate an Object being used as a key. 
- incorrect results, item gets lost 

Interesting Java HashMap implementation: once a bin gets too large, it turns into a red black tree

  

