- When creating a new `Collection<Node>[]` to store in our `buckets` variable, be aware that in Java, you [cannot create an array of parameterized type](https://docs.oracle.com/javase/tutorial/java/generics/restrictions.html#createArrays). `Collection<Node>` is a parameterized type, because we parameterize the `Collection` class with the `Node` class. Therefore, Java disallows `new Collection<Node>[size]`, for any given `size`. If you try to do this, you will get a “Generic array creation” error.

> To get around this, you should instead create a `new Collection[size]`, where `size` is the desired size.


