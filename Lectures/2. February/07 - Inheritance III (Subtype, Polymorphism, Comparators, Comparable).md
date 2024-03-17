### Static Methods, Variables, and Inheritance

- What if subclass has a static method with the same signature as a superclass method? 
	- For static methods, we do not use the term overriding for this

### Subtype Polymorphism

- Polymorphism: "providing a single interface to entities of different types"

Dynamic Method Selection = Subtype Polymorphism 

### Subtype Polymorphism vs. Explicit Higher Order Functions

```python
def print_larger(x, y, compare, stringify): # Explicit HoF Approach
	if compare(x, y): # sometimes called callback
		return stringify(x)
	return stringify(y)
```

```python
def print_larger(x, y): # Subtype Polymorphism Approach
	if x.largerThan(y):
		return x.str();
	return y.str();
```

### OurComparable
 
```java 
public interface OurComparable {
   public int compareTo(Object o);
}

public class Dog implements OurComparable {
   private String name;
   private int size;

   public int compareTo(Object o) {
       Dog uddaDog = (Dog) o;
       return this.size - uddaDog.size;
   }
}

public class Maximizer {
   public static Object max(Object[] items) {
		int maxDex = 0;
		for (int i = 0; i < items.length; i += 1) {
			int cmp = items[i].compareTo(items[maxDex]);
			if (cmp > 0) {
				maxDex = i;
			}
      }
      return items[maxDex];
   }
}
```

Java has its own Comparable interface that allows us to avoid awkward casting from Object because it uses generic type. 

## Comparators

The term "Natural Order" is sometimes used to refer to the ordering implied by a  Comparable's compareTo method. 

How can we change natural order with subtype polymorphism?

the answer: `comparator<T> c`. 

![[comparators.png]]

```java 
import java.utils.comparator;

// NameComparator Example

public class Dog implements Comparable<Dog> {
	private int size; 

	public int compareTo(Dog uddaDog) {
		return this.size - uddaDog.size;
	}

	private static class NameComparator implements Comparator<Dog> {
		public int compare(Dog d1, Dog d2) {
			return d1.name.compareTo(d2.name);
		}
	}

	public static Comparator<Dog> getNameComparator() {
		return new NameComparator(); 
	}
}

public class DogLauncher {
	public static void main(String[] args) { 
		Comparator<Dog> nc = Dog.getNameComparator(); 
		if (nc.compare(d1, d2) > 0) { // if d1 comes later than d2 in ABC
			d1.bark(); 
		} else {
			d2.bark(); 
		}
	}
}
```

**Summary:** 
![[comparablesummary.png]]

