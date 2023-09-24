# Concurrency Patterns

[[Active Object]]: Decouples method execution from method invocation on an object.
This pattern allows objects to have their methods invoked with a client's request, but the actual execution occurs asynchronously.

[[Balking]]: Used when an object's method is called in an inappropriate state. The method returns immediately without doing anything.

[[Barrier]]: Allows multiple threads to wait for each other to reach a common barrier point before proceeding.

[[Double-Checked Locking]]: Reduces the overhead of acquiring a lock by first testing the locking criterion without actually acquiring the lock.

[[Monitor Object]]: Synchronizes method execution to ensure that only one method is active on an object at once.

[[Read-Write Lock]]: Allows concurrent read access to an object but requires exclusive access for write operations.

[[Scheduler]]: Explicitly controls when threads execute.