# Core Java. Memory Management

## How GC works

### Detecting garbage

#### Reference Counting Approach

Every object has a counter of references. If the counter is 0, the object can be destroyed.

Mantaining such counter is hard, and it doesn't catch cycle references.

#### Tracing

There is some "root" object. If we can access some object from this root, the object is alive, otherwise it should be destroyed.

Possible roots:
* Local variables and method arguments
* Java threads
* Static variables
* JNI references

#### Garbage collection

##### Copying collectors

Memory is divided into parts named "from-space" and "to-space"

* Objects are allocated in from-space
* If from-space is full, the app is paused
* GC finds live objects in from-space and copies it to to-space
* from-space clears
* from-space and to-space swap

##### Mark-and-Sweep

* Objects are allocated in the memory
* When GC starts, the app is paused
* GC marks live objects in the object tree (Tracing)
* GC saves all non-marked pieces of memory in "free list"
* New objects are allocated in free list

Actual GC uses combination of both methods.

## Types of References

### Strong
Default reference type. If an object has a strong reference, it will never be garbage collected.

### Soft
Object can be collected if the app needs memory.

In Java it is used with `SoftReference` class. Value can be accessed with `get()` method, that returns `null` if it was collected.

Example of usage: image cache.

### Weak
Object may be collected even if the app has enough memory.

In Java it used with `WeakReference` class, which works similar way as `SoftReference`

Example of usage: 

* `WeakHashMap` — keys are stored as weak references, and the entry is destroyed if corresponding key is collected.
* Reference to `Context` or `Activity` in Android can be stored as weak reference to avoid memory leaks.

### Phantom

Java class `PhantomReference`. It is used with `ReferenceQuery`. 

At the first iteration GC calls `finalize()` and places the object to the reference queue. If a strong reference was not created, the object will be collected at the second GC iteration.

`get()` always returns null.