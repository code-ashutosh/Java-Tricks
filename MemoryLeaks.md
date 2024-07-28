
### What is Memory Leak?

```
Objects which are no longer required and garbage collector unable to remove them,
consumes heap memory contributing to memory leak.
 
It is responsibilty of Garbage collector to free heap memory from such objects.

Objects which are actually referenced but are unused keep consuming heap memory and contributes to memory leak
```

### Most Common Causes of Memory Leaks in Java

1. Excessive use of static members
2. Unclosed Resources
3. Improper equals and hashcode implementation
4. Excessive session objects
5. Poorly written custom data structures
<img width="1432" alt="Screenshot 2024-07-27 at 12 35 02 AM" src="https://github.com/user-attachments/assets/54305876-bd9b-403f-aacf-78c298be19cc">


### References
1. https://www.youtube.com/watch?v=1ksJpgk1HIc




### What is Garbage Collection?

1. Automatic process
2. Heap Area Cleanup
3. Identify and remove unused objects from memory. Memory used by unreferenced objects can be reclaimed during garbage collection.

   > Referenced Objects (Still in use)
   > Unreference Objects (No Longer in user)

### What is the need of GC ?

All objects are allocated memory on heap space.

1. Proper deallocation of memory.
2. Free up space for new objects.
3. Helps in preventing OutOfMemory Error by freeing up heap memory space.


### Process of GC

It's a 2 step process
- Marking unused objects
  All the referenced objects are skipped, but all the unreferenced objects are marked for removal

- Removal of unused objects
  1. Normal Removal : Referenced Objects will not be moved and fragmented free space will be available.
    
  2. Removal with compacting : Referenced Objects will be moved togather in the memory to make a contiguous free space block.

  3. Mark And Copy : Here we have Young Gen space(Y1) and a copy of it(Y2) , when minor GC is performed it marks the referenced objects and copy them to other Young Gen (Y2) and then clear the Y1 as a whole. It is faster than compacting.
 
### Object Allocation in Heap

1. New Objects will be allocated space in EDEN part

<img width="1432" alt="Screenshot 2024-07-27 at 1 48 44 PM" src="https://github.com/user-attachments/assets/56ceef96-efef-447e-aef1-4fefe0605a63">


2. Once EDEN starts filling up a minor GC occurs

<img width="1432" alt="Screenshot 2024-07-27 at 1 52 00 PM" src="https://github.com/user-attachments/assets/1da47b5d-94f1-42c7-a7e3-c0497dcb2c13">

3. In **Minor GC** unreferenced objects are marked and removed whereas referenced objects are moved to **S0 Survivor** plus aging factor in incremented.

<img width="1432" alt="Screenshot 2024-07-27 at 1 53 00 PM" src="https://github.com/user-attachments/assets/5a72d718-9c81-4f8a-a232-d32ad8b8441b">

4. Object Ageing (Every time a GC occurs aging factor of survivors will increase) 

In below example 1 & 2 denotes aging (or number of GC survived by objects)

<img width="1432" alt="Screenshot 2024-07-27 at 1 54 57 PM" src="https://github.com/user-attachments/assets/bdbcc40b-2e27-4c5c-84ad-2214a7970afe">


5. Promotion of Referenced Objects from Young Generation to Old Generation

Objects which survived multiple GC are then promoted to OLD Gen space



<img width="1432" alt="Screenshot 2024-07-27 at 1 58 00 PM" src="https://github.com/user-attachments/assets/1573d2c0-d04f-4a2e-9f94-dd185c05b988">

6. A Major GC will occur when Old Gen space starts filling, and cleans Old Gen.

<img width="1432" alt="Screenshot 2024-07-27 at 1 59 40 PM" src="https://github.com/user-attachments/assets/08d22da2-ea78-46b4-9603-b76396f97792">


### Relation between Object Aging and Memory Leak

<img width="1432" alt="Screenshot 2024-07-28 at 7 47 18 PM" src="https://github.com/user-attachments/assets/acfbc40b-9999-4c08-be3c-cedf77679e7f">


### Common JVM Commands to specify the different parts of heap size

<img width="1432" alt="Screenshot 2024-07-27 at 2 01 14 PM" src="https://github.com/user-attachments/assets/43f0c1ad-96a6-4b98-bc7a-dd1c576f608a">

<img width="1432" alt="Screenshot 2024-07-27 at 2 02 14 PM" src="https://github.com/user-attachments/assets/0d5d70da-f89a-44ac-9cd2-e3cd2726286c">

<img width="1432" alt="Screenshot 2024-07-27 at 2 02 28 PM" src="https://github.com/user-attachments/assets/10c49d1f-d3c3-4932-8c69-9f0bc68254d9">


NOTE: Permament Gen (Meta Space post java 8) is part of heap space where permanent objects like static objects or config objects are kept

<img width="1432" alt="Screenshot 2024-07-27 at 2 02 42 PM" src="https://github.com/user-attachments/assets/438c643d-a474-4e08-8b97-834fe609e2eb">




### Types of Garbage Collectors in  Java

There are 5 types of GC avaialble

1. Serial GC
2. Parallel GC
3. Cuncurrent Mark Sweep (CMS)
4. G1 (Garbage First)
5. Z GC

> **Stop The World** : The application is frozen till the GC is done. All the threads of application are paused.


#### 1. Serial GC
<img width="1432" alt="Screenshot 2024-07-27 at 2 13 36 PM" src="https://github.com/user-attachments/assets/eacb05d0-bff3-4e4d-90d6-149453d4cbfa">

#### 2. Parallel GC

It also uses `Stop The World` event but since multiple threads are doing mark and copy so time window of `Stop The World` event is small.
<img width="1432" alt="Screenshot 2024-07-27 at 2 15 48 PM" src="https://github.com/user-attachments/assets/effdc631-67a0-41d7-aebe-351a8961732a">


#### 3. Cuncurrent Mark Sweep (CMS)
<img width="1432" alt="Screenshot 2024-07-27 at 2 19 21 PM" src="https://github.com/user-attachments/assets/90e58143-70ec-4a4f-8ca9-3862583967ec">




#### 4. G1 (Garbage First) 

- Added in java 7
- It is best choice for many applications

<img width="1432" alt="Screenshot 2024-07-27 at 2 20 05 PM" src="https://github.com/user-attachments/assets/623db567-9b3f-449b-a78c-c752d9f92092">


#### 5. Z GC

- Added in java 15
- Works only on 64 bit system.

<img width="1432" alt="Screenshot 2024-07-27 at 2 21 10 PM" src="https://github.com/user-attachments/assets/4c988609-b081-45ca-a176-5e4d23316cf0">





### Performance Impact of GC on application


Whenever the GC occurs a spike comes in CPU usage.


<img width="1432" alt="Screenshot 2024-07-27 at 2 22 56 PM" src="https://github.com/user-attachments/assets/73127758-4202-4129-acbe-1052966eee48">

### GC Metrics

<img width="1432" alt="Screenshot 2024-07-27 at 2 26 08 PM" src="https://github.com/user-attachments/assets/e7de2658-d18a-4cb8-ab5b-f0e6d2ae46d2">


1. Allocation Rate: How fast your application is allocating object in the memory
2. Heap Population: Amount of objects that are residing in the heap at any point of time.
3. Mutation Rate: How often references are updated in the memory.
4. Life of Objects: How long an object typically living.
5. Mark Time: Time required by GC in marking the live objects 
6. Compaction Time : Time required by GC in which GC reallocates the objects and free up space.
7. GC cycle Time: Mark Time + Copact Time, i.e total time taken by GC.

### GC Tuning

<img width="1432" alt="Screenshot 2024-07-27 at 2 33 03 PM" src="https://github.com/user-attachments/assets/4f968a4d-f667-46e7-9cde-8c38237ef6a0">



### Healthy Heap Example

Here after each GC memory is reclaimed
<img width="1432" alt="Screenshot 2024-07-27 at 2 33 46 PM" src="https://github.com/user-attachments/assets/e7d004b9-2df1-48ea-95d8-9c7983950ecc">

### UnHealthy Heap Example

Here even after each GC memory is not reclaimed completely and increases gradually

<img width="1432" alt="Screenshot 2024-07-27 at 2 34 08 PM" src="https://github.com/user-attachments/assets/709618ce-f824-424c-9954-2b3266c0277e">


### How to Improve GC performance


<img width="1432" alt="Screenshot 2024-07-27 at 2 35 55 PM" src="https://github.com/user-attachments/assets/2b119d2f-3bbd-49cc-8606-da5e0d89aa10">


1. If we increase the Young Gen then minor GC will occur less frequently but will take more time as it needs to scan larger memory for marking and cleanup so timetaken will be larger.

2. If we decrease the Young Gen then GC will occur very fast  as it needs to scan small part of memory, but more frequent GC will happen as the small memory (Young Gen) will be filled frequently

3. Processing the streams directly : It means the if we have a file which is on unpredictable size we should not store it rather process it with the help of stream

### How to enable Different Types of GC

<img width="1432" alt="Screenshot 2024-07-27 at 2 44 37 PM" src="https://github.com/user-attachments/assets/7d4a7993-1387-4284-92c9-77be1aa6d085">



### References:

- https://www.youtube.com/watch?v=ZMaQDFTbWOo&list=PLOktGWstEblqNOq05Kj6YIdkEAz6Ktv60&index=12
- https://www.youtube.com/watch?v=E2KYTXKUsT4




