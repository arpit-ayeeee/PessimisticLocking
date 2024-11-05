# Pessimistic Locking Demonstration using Mutex

This repository demonstrates **pessimistic locking** in Go using **mutexes**. The code highlights the differences in behavior when incrementing a shared counter variable with and without using a mutex lock to manage concurrency.

## Introduction

Concurrency issues arise when multiple threads or goroutines access and modify shared resources simultaneously without proper synchronization. This can lead to data races and incorrect results. One way to avoid such issues is by using pessimistic locking, where we explicitly lock a resource (in this case, a shared counter) to prevent concurrent access by other threads until the lock is released.

### Problem Demonstrated

- **Without Locking**: Multiple goroutines increment a shared counter variable concurrently. Without a lock, the final count will likely be incorrect due to race conditions.
- **With Mutex Locking**: Each goroutine locks the counter before modifying it, ensuring that only one goroutine can access the shared resource at a time, thus maintaining data consistency.

## Code Overview

The program runs two scenarios:

1. **Incrementing the counter without any locking.**
2. **Incrementing the counter with mutex locking.**

### Functions:

- `incCountWithoutLock(wg *sync.WaitGroup)`: Increments the counter without any locking. This demonstrates a race condition where multiple goroutines modify the shared counter simultaneously.
- `incCountWithMutex(wg *sync.WaitGroup)`: Increments the counter using a mutex lock to ensure that only one goroutine modifies the shared counter at any given time.
- `countWithoutLock()`: Spawns multiple goroutines to increment the counter without locking and waits for all to finish.
- `countWithMutex()`: Spawns multiple goroutines to increment the counter with mutex locking and waits for all to finish.

## How to Run

1. Clone the repository.
2. Build and run the Go program:

   ```bash
   go run main.go
   ```

3. Observe the difference in the final counter value for both cases.

### Expected Output:

- **Without Lock**: The final count is expected to be incorrect due to race conditions (likely less than the intended number of increments).
- **With Mutex**: The final count should be accurate and equal to the number of threads (`NUM_THREADS`), as mutex locking ensures proper synchronization.

```bash
count (without lock) <some incorrect value>
count (with mutex) 1000000
```

## Key Concepts:

### Mutex
- A **mutex** (mutual exclusion) is a synchronization primitive used to protect shared resources in concurrent environments. It ensures that only one thread can access the critical section (the portion of code modifying shared data) at a time.

### Pessimistic Locking
- In this demo, pessimistic locking is achieved using the mutex. It "pessimistically" assumes that conflicts will occur, so it locks the resource before modifying it to prevent any concurrent access by other goroutines.

## Conclusion

This demo shows how mutexes can be used to ensure data integrity in concurrent programming by preventing race conditions. The pessimistic locking approach using a mutex guarantees that shared resources are accessed safely in a multi-threaded environment.