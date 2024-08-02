

### Role of `queueCapacity` and `maxPoolSize` in `ThreadPoolTaskExecutor`

1. **`queueCapacity`**:
   - This parameter defines the size of the queue that holds tasks before they are executed.
   - When the number of active threads reaches the `corePoolSize`, new tasks are placed in the queue.
   - If the queue is full, new tasks will be handled according to the `RejectedExecutionHandler` policy (default is `AbortPolicy` which throws a `RejectedExecutionException`).

2. **`maxPoolSize`**:
   - This parameter defines the maximum number of threads that can be created in the pool.
   - When the queue is full and the number of active threads is less than `maxPoolSize`, new threads are created to handle the tasks.
   - If the number of active threads reaches `maxPoolSize` and the queue is full, new tasks will be rejected according to the `RejectedExecutionHandler` policy.

### Pseudocode
1. **Task Submission**:
   - Submit a task to the executor.
   - If the number of active threads is less than `corePoolSize`, create a new thread to handle the task.
   - If the number of active threads is equal to or greater than `corePoolSize`, place the task in the queue.

2. **Queue Handling**:
   - If the queue is not full, place the task in the queue.
   - If the queue is full and the number of active threads is less than `maxPoolSize`, create a new thread to handle the task.
   - If the queue is full and the number of active threads is equal to or greater than `maxPoolSize`, reject the task according to the `RejectedExecutionHandler` policy.

### Code Example
```java
@Bean(name = "sqsAsyncExecutor")
public ThreadPoolTaskExecutor sqsAsyncExecutor() {
    ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
    executor.setCorePoolSize(5); // Minimum number of threads to keep in the pool
    executor.setMaxPoolSize(10); // Maximum number of threads in the pool
    executor.setQueueCapacity(10000); // Size of the queue to hold tasks before they are executed
    executor.setThreadGroupName("sqsAsyncExecutor");
    executor.setThreadNamePrefix("sqsAsyncExecutor-");
    executor.initialize();
    return executor;
}
```
