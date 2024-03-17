Short summary: 
1. DLList can't get i index
2. The Naive AList: a class that works with items array with functionality similar to DLList
3. The allegory of the cave: the raw data of the array might differ from what user thinks (the last item is not deleted, size changes only)
4. Resizing arrays: System.arraycopy into a bigger array

![[resize.png]]

5. Problem with resize: incrementing the size by just 1 results in a slow array. SLList is faster. 
6. The solution: geometric resizing is much faster. This is how the Python list is implemented.

![[arrayefficiency.png]]

7. Java quirk: you can't instantiate a Generic type array

![[genericalist.png]]

8. When AList is not integer based, we want to null out deleted items since they can be heavy in memory. Not doing so called loitering (not deleted objects). 

## AList implementation: 

```java
/* Invariants: 
    addLast: The next item we want to add, will go into position "size"
    size: number of items in the list should be size.
    getLast: the item we want to return is in position "size - 1"

*/

public class AList<Glorp> {
    /* prevent outsider from manipulating => private */
    private Glorp[] items;
    private int size;
    private double usage_ratio;

    /* Constructor - create empty list: define memeory boxes */
    public AList(){
	    items = (Glorp []) new Object[10];
        size = 0;
    }

    /* make a indep, private method to help in resizing the array
    Can test the component independently, and easier to read */
    private void resize_array(int capacity){
        Glorp[] new_array = (Glorp []) new Object[capacity];
        System.arraycopy(items, 0, new_array, 0, size);
        items = new_array;
    }

    public void addLast(Glorp x){
        /* Make it dynamic */
        if (size == items.length){
            /* resizing factor => using mal is better than add */
            resize_array(size * 2);
        }

        /* "size" acts like the index for the last item */
        items[size] = x;
        size += 1;
    }

    public int getLast(){
        return items[size - 1];
    }

    public int get(int i){
        return items[i];
    }

    public int size(){
        return size;
    }

    public int removeLast(){
        /* setting deleted item to 0: not necessary to 
        preserve invariants */
        Glorp x = getLast();
        size -= 1;

        usage_ratio = size * 1.0 / items.length;
        if (usage_ratio < 0.25){
            resize_array(items.length / 2);
        }

        return x;
    }

    public static void main(String[] args) {

    }
}
```