Today's Goal: Build an implementation of a Set called ArraySet. 
### Exceptions
```java 
if (x == null) {
	throw new IllegalArgumentException("can't add null to an ArraySet");
	// should be try catch 
}
```

## The Enhanced For Loop 

```java 
// pretty iterator
Set<Integer> javaset = new HashSet<>();

for (int i: javaset) {
	System.out.println(i);
}

// ugly iterator 
Iterator<Integer> seer = javaset.iterator(); // don't forget to import

while (seer.hasNext()) {
	int i = seer.next();
	System.out.println(i);
}
```

Our implementation: 
```java
public class ArraySet implements Iterable<T> {
	// starting code of addNext and contains methods  

	public Iterator<Integer> iterator() {
		return new ArraySetIterator();
	}

	private class ArraySetIterator implements Iterator<T> { 
		private int wizPos; 
		public ArraySetIterator() {
			wizPos = 0; 	
		}
	
		public boolean hasNext() {
			return wizPos < size;
		}

		public T next() {
			T returnItem = items[wizPos];
			wizPos += 1; 
			return returnItem;
		}
	}

	public static void main(String[] args) {
		ArraySet<Integer> aseer = new ArraySet<>(); 
		Iterator<Integer> aseer = aset.iterator();
		while (aseer.hasNext()) {
			int i = aseer.next();
			System.out.println(i);	
		}
	}
}
```

Even with this ugly implementation, our nice iteration will not work by itself. Our ArraySet should implement `Iterable<T>` first. That interface has `iterator()` method.  

To support the enhanced for loop: 
- Add an `iterator()` method to your class that returns an `Iterator<T>`
- The `Iterator<T>` returned should have a useful `hasNext()` and `next()` methods
- Add `implements Iterable<T>` to the line defining your class 


## Object Methods: toString() and Equals

Warning: this code is slow because Strings are "immutable". 
```java 
@Override
   public String toString() {
       String returnString = "{";
       for (T item : this) {
           returnString += item; // might not be a string, but Java automatically calls .toString 
           returnString += ", ";
       }
       returnString += "}";
       return returnString;
   }
```

Much faster approach is shown below. 
- Intuition: append operation for a StringBuilder is fast 
``` java
@Override
public String toString() {
   StringBuilder returnSB = new StringBuilder("{");
   
   for (int i = 0; i < size - 1; i += 1) {
       returnSB.append(items[i]); // again, .toString is automatic
       returnSB.append(", ");
   }
   returnSB.append(items[size - 1]); // to avoid one odd comma 
   returnSB.append("}");
   return returnSB.toString();
}
```

### Equals vs. == 
- == compares the bits. For references, == means "referencing the same object"
- To test the equality of classes, implement `.equals`
	- default of implementation of `.equals` uses ==
- BTW: use `Arrays.equal` or `Arrays.deepEquals` for arrays 

### this
- If there’s ever a name conflict where a local variable has the same name as an instance variable (left), you must use this if you want to access the instance variable.

### instanceOf 

![[insatnceof.png]]

### ArraySet implementation of equals
```java 
	@Override
   public boolean equals(Object o) {
		if (this == other) {return true; } // for performance 

       if (o instanceof ArraySet oas) {
           // check sets are of the same size
           if (oas.size != this.size) {
               return false;
           }

           // check that all of MY items are in the other array set
           for (T x : this) {
               if (!oas.contains(x)) {
                   return false;
               }
           }

           return true;
       }

       // o is not an arrayset, so return false
       return false;
   }
```


