
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
