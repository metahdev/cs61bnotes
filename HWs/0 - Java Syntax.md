|Python|Java|What?|
|---|---|---|
|`bool`|`boolean`|Python uses `True` and `False`; Java uses `true` and `false`.|
|`int`|`int`|While Python `int`s are unbounded, Java `int`s have a (large) max and min value.|
|`float`|`double`|Decimal values. Java `doubles` are again bounded.|
|`str`|`String`|Java `String`s use double quotes (`"`), and can be any text.|
|no equivalent|`char`|Java `char` represents a _single_ character, and uses single quotes (`'`).|


- NOTE: In Java, `==` is used for identity, and `.equals()` is used for equality. For primitive types, this means the same thing, but for reference types, it may be different. For this assignment, you do not need to know the difference; we’ll learn more about this later.

```java
int x = Math.pow(2, 10);
```


```Java
String s = "hello";
s += " world";

s += 5; // In Java, you can add anything to a `String`s, and it will be implicitly converted to a `String` without needing to explicitly cast.

int sLength = s.length();
String substr = s.substring(1, 5); 

char c = s.charAt(2);

if (s.indexOf("hello") != -1) { // if "hello" in s 
    System.out.println("\"hello\" in s");
}

for (int i = 0; i < s.length(); i++) {
    char letter = s.charAt(i);
    System.out.println(letter);
}
```

### Number Total problem 

Don't forget that the loop condition is being checked continuously.

``` java
public class MyClass {
    public static void main(String args[]) {
        int total = 25;
        for (int number = 1; number <= (total / 2); number++) {
            total = total - number;
            System.out.println(total + " "+ number);
        }
    }
}

/*
24 1
22 2
19 3
15 4
10 5
*/
```

### Foreach Loop / Enhanced For Loop

```python
lst = [1, 2, 3]
for i in lst: 
	print(i)
```

```java 
int[] array = {1, 2, 3};
for (int i: array) {
	System.out.println(i);
}
```

``` java 
// RESIZABLE LIST
List<String> lst = new ArrayList<>();
lst.add("zero");
lst.add("one");
lst.set(0, "zed");
System.out.println(lst.get(0)); 
System.out.println(lst.size());
if (lst.contains("one")) {
    System.out.println("one in lst");
}
for (String elem : lst) {
    System.out.println(elem);
}
```

### Sets

- Java has the `Set` interface. There are two main implementations: [`TreeSet`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/TreeSet.html), and [`HashSet`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/HashSet.html). `TreeSet` keeps its elements in “sorted” order, and is fast. In contrast, `HashSet` does not have a defined “order”, but is (usually) really fast.
    - We will formalize these notions of “fast” later on in the course when we learn about asymptotic analysis.
- A `Set` cannot contain duplicate items. If we try to add an item already in the set, nothing happens.

```java
Set<Integer> set = new HashSet<>();
set.add(1);
set.add(1);
set.add(2);
set.remove(2);
System.out.println(set.size());
if (set.contains(1)) {
    System.out.println("1 in set");
}
for (int elem : set) {
    System.out.println(elem);
}
```

### Dictionaries / Maps

```java
Map<String, String> map = new HashMap<>();
map.put("hello", "hi");
map.put("hello", "goodbye");
System.out.println(map.get("hello"));
System.out.println(map.size());
if (map.containsKey("hello")) {
    System.out.println("\"hello\" in map");
}
for (String key : map.keySet()) {
    System.out.println(key);
}
```

- Java has the `Map` interface. There are two main implementations: [`TreeMap`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/TreeMap.html), and [`HashMap`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/HashMap.html). Similarly to sets, `TreeMap` keeps its keys sorted and is fast; `HashMap` has no defined order and is (usually) really fast.
- A `Map` cannot contain duplicate keys. If we try to add a key already in the map, the value is overwritten.
- In the angle brackets, we have the “key type” first, followed by the “value type”.
- `Map`s cannot directly be used with the `:` for loop. Typically, we call `keySet` to iterate over a set of the keys, and use those to retrieve the values. One may also iterate over the `entrySet` to get both the keys and values.

### Exceptions

```java
throw new Exception("There are no elements in the array!");
```

