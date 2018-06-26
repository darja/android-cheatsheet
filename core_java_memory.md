# Core Java. Memory Management

## How GC works

## Types of References
* *Strong* -- default reference type. If an object has a strong reference, it will never be garbage collected
* *Soft* -- object can be collected if the app needs memory
* *Weak* -- object may be collected even if the app has enough memory
* *Phantom* -- used with `ReferenceQuery`. GC at the first iteration calls `finalize()` and places the object to the reference queue. If a strong reference was not created, the object will be collected at the second GC iteration. `get()` always returns null.