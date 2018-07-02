# Core Java. Multithreading

## Threads

*Process* is an instance of a computer program that is being executed

*Thread* is a sequence of instructions that exist in the process. Several threads can be executed in parallel. They have their own stack and variables, but also can access shared memory.

###Creating

In Java we have `Runnable` class, that is actually a wrapper for a void function. We can create `Thread` object passing some `Runnable` object as an argument. Then we call `start` and code in Runnable starts executing in separate thread.

```java
Runnable task = () -> {
    System.out.println("Hello " + Thread.currentThread().getName());
};

Thread thread = new Thread(task);
thread.start();
```

###Stopping

`interrupt()` method of `Thread` can be used for stopping a thread. It doesn't stop the thread, but sets `isInterrupted` flag. Also, if the thread is sleeping, it throws `InterruptedException`.

So, `run` method of Runnable should sometimes check `isRunnable` and catch `InterruptedException`.

## Executors
`ExecutorService` is more high-level way to run asynchronous tasks. It provides easy creation of thread pool and assigning tasks to it.

```java
ExecutorService executorService = Executors.newFixedThreadPool(10);
executorService.execute(() -> {
    System.out.println("Hello " + Thread.currentThread().getName());
});
executorService.shutdown();
```

### Running Tasks
There are different ways to run tasks in `ExecutorService`:

* `execute(Runnable)` — executing void function
* `submit(Runnable)` — also executes void function, but returns a `Future` object, that can be used to check if the Runnable as finished executing.
* `submit(Callable)` — executes `Callable` (wrapper to non-void function), also returns `Future`, which we can use to receive result.
* `invokeAny(...)` — takes a collection of Callables and starts to execute them. Once one of them is finishes the others are cancelled and result of executed one is returned.
* `invokeAll(...)` — executes all callables in the collection passed as argument. Returns `List<Future>` that can be used to obtain results.

### Stopping
When `ExecutorService` finishes its work, it doesn't destroy itself. So, when you are done using it you should shut it down. That can be done with following methods:

* `shutdown()` — `ExecutorService` stops accepting new tasks and destroys itself after the last task is over.
* `shutdownNow()` — tries to destroy `ExecutorService` immediately, returns list of tasks that are not yet executed.

It is recommended to use both ways with `awaitTermination` call:

```java
executorService.shutdown();
try {
    if (!executorService.awaitTermination(800, TimeUnit.MILLISECONDS)) {
        executorService.shutdownNow();
    } 
} catch (InterruptedException e) {
    executorService.shutdownNow();
}
```

## Synchronized blocks and methods

Synchronized block can guarantee that only one thread can run its code.

In Java `synchronized` keyword require a parameter called monitor. While a monitor is locked by synchronized block, no other thread can access related code.   

`synchronized` can be used for method declaration. It is the same as synchrotized block that uses `this` (or `class` object, if the method is static) as monitor.

## Wait/Notify Mechanism
`wait`, `notify` and `notifyAll` methods are defined in `Object` class.

If some thread calls `wait`, it is suspended until some other thread calls `notify` or `notifyAll`. `notify` awakes any of the waiting threads, `notifyAll` awakes all of them. `wait` also has an option to pass timeout.

Example of wait/notify usage: thread pool.