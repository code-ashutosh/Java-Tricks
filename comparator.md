
### How does compare method works internally explain with example in detail ?

Sure, let's delve into how the `compare` method works internally, especially within the context of sorting. I'll explain it with an example of sorting a list of integers.

1. **Understanding the Comparator Interface**:

   In Java, the `Comparator` interface is used to define custom comparison logic. It has a single method `compare(T o1, T o2)` that compares two objects of type `T`. The `compare` method returns an integer:
   - Negative integer: If `o1` is less than `o2`.
   - Zero: If `o1` is equal to `o2`.
   - Positive integer: If `o1` is greater than `o2`.

2. **Sorting with a Comparator**:

   When you sort a collection, like a list, using a `Comparator`, the sorting algorithm uses the `compare` method to determine the order of elements.

3. **Example**:

   Let's say we have a list of integers: `[5, 2, 8, 1, 3]`. We want to sort this list in ascending order.

   We can define a comparator to compare integers like this:

   ```java
   Comparator<Integer> comparator = new Comparator<Integer>() {
       @Override
       public int compare(Integer o1, Integer o2) {
           return o1.compareTo(o2); // Uses Integer's natural ordering
       }
   };
   ```

   Here, `o1.compareTo(o2)` invokes the `compareTo` method of the `Integer` class, which internally handles the comparison.

4. **Sorting the List**:

   We can use `Collections.sort()` method to sort the list using the comparator:

   ```java
   List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 3);
   Collections.sort(numbers, comparator);
   ```

   When `Collections.sort()` is called, it internally uses the `compare` method defined in the `comparator` object to determine the order of elements in the list.

5. **Execution**:

   - The sorting algorithm (usually a variation of quicksort or mergesort) repeatedly calls the `compare` method provided by the comparator.
   - The `compare` method returns the result of the comparison between two integers.
   - Based on the result, the sorting algorithm rearranges the elements in the list until they are in the desired order.

6. **Result**:

   After sorting, the list `[5, 2, 8, 1, 3]` becomes `[1, 2, 3, 5, 8]` according to the natural order of integers.

In summary, the `compare` method is the heart of sorting when using a `Comparator` in Java. It defines how elements should be compared and allows the sorting algorithm to arrange them accordingly.
