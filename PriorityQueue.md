# Java Collections


### Heap (Priority Queue)
1. Min heap  -> smallest element is at the top

```
Queue<Integer> minHeap = new PriorityQueue<>();
```
or

```
Queue<Integer> minHeap = new PriorityQueue<>((a,b) -> a-b)
```

2. Max heap  -> largest element is at the top

```
Queue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
```

or
```
Queue<Integer> maxHeap = new PriorityQueue<>((a,b) -> b-a)
```
---
### Comparator working 

The `Comparator` provided in the `PriorityQueue` constructor `(a, b) -> a - b` is a lambda expression that defines how the elements in the queue are ordered. Here's a step-by-step explanation of how it works:

1. **Lambda Expression**: `(a, b) -> a - b` is a lambda expression that takes two arguments `a` and `b` (both of type `Integer` in this context) and returns the result of `a - b`.
2. **Comparator Logic**: The result of `a - b` determines the order of elements in the priority queue (min-heap in this case).
   - If `a - b` is **negative**, `a` is considered less than `b`, and `a` should come before `b` in the queue.
   - If `a - b` is **positive**, `a` is considered greater than `b`, and `a` should come after `b` in the queue.
   - If `a - b` is **zero**, `a` and `b` are considered equal in terms of ordering, and their order relative to each other is not guaranteed.
3. **Min-Heap Property**: Because the comparator is defined as `(a, b) -> a - b`, the smallest element (according to the natural ordering of `Integer`) will be at the head of the queue. This is because elements for which the comparator returns a smaller value are given priority.

In summary, this comparator ensures that the `PriorityQueue` acts as a min-heap, where the element with the lowest value is always at the front of the queue, and elements are removed in ascending order.

---

#### Common use cases [https://favtutor.com/blogs/learn-about-priority-queue-in-java-and-about-its-methods-with-different-examples]

###### 1. Adding Elements to a Priority Queue

> To add elements to a priority queue, we can use the add(E element) or offer(E element) methods. Both methods insert the specified element into the priority queue. If the queue is full, the add() method throws an exception, while the offer() method returns false.

```
priorityQueue.add(10);
priorityQueue.offer(20);
```
###### 2. Accessing Elements in a Priority Queue

> To access the elements in a priority queue, we can use the peek() method. This method retrieves, but does not remove, the head of the queue, i.e., the element with the highest priority.


```
Integer element = priorityQueue.peek();
```


###### 3. Removing Elements from a Priority Queue

> To remove elements from a priority queue, we can use the poll() method. This method retrieves and removes the head of the queue, i.e., the element with the highest priority. If the queue is empty, the poll() method returns null.

```
Integer element = priorityQueue.poll();
```




###### 4. Custom Ordering

> If you want to order the elements in the priority queue based on a custom ordering, you can provide a custom comparator to the constructor. A comparator is an object that compares two elements and determines their order. You can define your own comparator by implementing the Comparator interface. Here's an example of creating a priority queue with a custom comparator that orders strings based on their length:
 
```
PriorityQueue<String> priorityQueue = new PriorityQueue<>(Comparator.comparingInt(String::length));
```

###### Example 1:

```
PriorityQueue<String> taskQueue = new PriorityQueue<>();
taskQueue.add("High priority task");
taskQueue.add("Medium priority task");
taskQueue.add("Low priority task");

while (!taskQueue.isEmpty()) {
String task = taskQueue.poll();
System.out.println("Processing task: " + task);
}
```

##### 5. Pririty Queue of Pair (Max Heap)

```java
PriorityQueue<Pair<Integer, Double>> pq = new PriorityQueue<>((a,b) -> Double.compare(b.getValue(), a.getValue()));
```


#### Java Priority Blocking Queue (Thread Safe)
In a multi-threaded environment, it's important to ensure thread safety when using a priority queue. The PriorityQueue class in Java is not thread-safe. However, Java provides the PriorityBlockingQueue class, which is an implementation of the BlockingQueue interface and offers thread-safe operations on a priority queue.

The PriorityBlockingQueue class provides all the functionality of a priority queue while ensuring thread safety. It allows multiple threads to access and modify the queue concurrently without the need for external synchronization.

To use a PriorityBlockingQueue, you can create an instance of it and use the same methods as a regular priority queue.

```
PriorityBlockingQueue<Integer> priorityQueue = new PriorityBlockingQueue<>();
priorityQueue.add(10);
priorityQueue.add(20);

Integer element = priorityQueue.poll();
```


