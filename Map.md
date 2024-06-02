### Java MAP Interface


#### Iterating Over a Map

There are generally 5 ways of iterating over a `Map` in Java

First of all, `we cannot iterate a Map directly using iterators, because Map are not Collection`. Also before going further, you must know a little-bit about Map.Entry<K, V> interface.
Since all maps in Java implement Map interface, following techniques will work for any map implementation (HashMap, TreeMap, LinkedHashMap, Hashtable, etc.)

**1. Iterating over Map.entrySet() using For-Each loop :**
```java
// Java program to demonstrate iteration over 
// Map.entrySet() entries using for-each loop 

import java.util.Map; 
import java.util.HashMap; 

class IterationDemo 
{ 
	public static void main(String[] arg) 
	{ 
		Map<String,String> gfg = new HashMap<String,String>(); 
	
		gfg.put("GFG", "geeksforgeeks.org"); 
		gfg.put("Practice", "practice.geeksforgeeks.org"); 
		gfg.put("Code", "code.geeksforgeeks.org"); 
		gfg.put("Quiz", "www.geeksforgeeks.org"); 
		
		// using for-each loop for iteration over Map.entrySet() 
		for (Map.Entry<String,String> entry : gfg.entrySet()) 
			System.out.println("Key = " + entry.getKey() + 
							", Value = " + entry.getValue()); 
	} 
} 
```
**2. Iterating over keys or values using keySet() and values() methods:**

Map.keySet() method returns a Set view of the keys contained in this map and Map.values() method returns a collection-view of the values contained in this map. So If you need only keys or values from the map, you can iterate over keySet or values using for-each loops. Below is the java program to demonstrate it.
```java
// Java program to demonstrate iteration over 
// Map using keySet() and values() methods 

import java.util.Map; 
import java.util.HashMap; 

class IterationDemo 
{ 
	public static void main(String[] arg) 
	{ 
		Map<String,String> gfg = new HashMap<String,String>(); 
	
		// enter name/url pair 
		gfg.put("GFG", "geeksforgeeks.org"); 
		gfg.put("Practice", "practice.geeksforgeeks.org"); 
		gfg.put("Code", "code.geeksforgeeks.org"); 
		gfg.put("Quiz", "www.geeksforgeeks.org"); 
		
		// using keySet() for iteration over keys 
		for (String name : gfg.keySet()) 
			System.out.println("key: " + name); 
		
		// using values() for iteration over values 
		for (String url : gfg.values()) 
			System.out.println("value: " + url); 
	} 
} 
```
**3. Iterating using iterators over Map.Entry<K, V>:**
This method is somewhat similar to first one. In first method we use for-each loop over Map.Entry<K, V>, but here we use iterators. Using iterators over Map.Entry<K, V> has it’s own advantage,i.e. we can remove entries from the map during iteration by calling iterator.remove() method.
```java
// Java program to demonstrate iteration over 
// Map using keySet() and values() methods 

import java.util.Map; 
import java.util.HashMap; 
import java.util.Iterator; 

class IterationDemo 
{ 
	public static void main(String[] arg) 
	{ 
		Map<String,String> gfg = new HashMap<String,String>(); 
	
		// enter name/url pair 
		gfg.put("GFG", "geeksforgeeks.org"); 
		gfg.put("Practice", "practice.geeksforgeeks.org"); 
		gfg.put("Code", "code.geeksforgeeks.org"); 
		gfg.put("Quiz", "www.geeksforgeeks.org"); 
		
		// using iterators 
		Iterator<Map.Entry<String, String>> itr = gfg.entrySet().iterator(); 
		
		while(itr.hasNext()) 
		{ 
			Map.Entry<String, String> entry = itr.next(); 
			System.out.println("Key = " + entry.getKey() + 
								", Value = " + entry.getValue()); 
		} 
	} 
} 

```


**4. Using forEach(action) method :**
In Java 8, you can iterate a map using Map.forEach(action) method and using lambda expression. This technique is clean and fast.

```java
// Java code illustrating iteration 
// over map using forEach(action) method 

import java.util.Map; 
import java.util.HashMap; 

class IterationDemo 
{ 
	public static void main(String[] arg) 
	{ 
		Map<String,String> gfg = new HashMap<String,String>(); 
	
		// enter name/url pair 
		gfg.put("GFG", "geeksforgeeks.org"); 
		gfg.put("Practice", "practice.geeksforgeeks.org"); 
		gfg.put("Code", "code.geeksforgeeks.org"); 
		gfg.put("Quiz", "www.geeksforgeeks.org"); 
		
		// forEach(action) method to iterate map 
		gfg.forEach((k,v) -> System.out.println("Key = "
				+ k + ", Value = " + v)); 
		
	} 
} 

```

**5. Iterating over keys and searching for values (inefficient):**
Here first we loop over keys(using Map.keySet() method) and then search for value(using Map.get(key) method) for each key.This method is not used in practice as it is pretty slow and inefficient as getting values by a key might be time-consuming.

```java
// Java program to demonstrate iteration 
// over keys and searching for values 

import java.util.Map; 
import java.util.HashMap; 

class IterationDemo 
{ 
	public static void main(String[] arg) 
	{ 
		Map<String,String> gfg = new HashMap<String,String>(); 
	
		// enter name/url pair 
		gfg.put("GFG", "geeksforgeeks.org"); 
		gfg.put("Practice", "practice.geeksforgeeks.org"); 
		gfg.put("Code", "code.geeksforgeeks.org"); 
		gfg.put("Quiz", "www.geeksforgeeks.org"); 
		
		// looping over keys 
		for (String name : gfg.keySet()) 
		{ 
			// search for value 
			String url = gfg.get(name); 
			System.out.println("Key = " + name + ", Value = " + url); 
		} 
	} 
} 

```


#### Sort A Map By Value

```java
public static HashMap<String, Integer> sortByValue(HashMap<String, Integer> hm)
    {
        // Create a list from elements of HashMap
        List<Map.Entry<String, Integer> > list =
               new LinkedList<Map.Entry<String, Integer> >(hm.entrySet());
 
        // Sort the list
        Collections.sort(list, new Comparator<Map.Entry<String, Integer> >() {
            public int compare(Map.Entry<String, Integer> o1, 
                               Map.Entry<String, Integer> o2)
            {
                return (o1.getValue()).compareTo(o2.getValue());
            }
        });
         
        // put data from sorted list to hashmap 
        HashMap<String, Integer> temp = new LinkedHashMap<String, Integer>();
        for (Map.Entry<String, Integer> aa : list) {
            temp.put(aa.getKey(), aa.getValue());
        }
        return temp;
    }
```
