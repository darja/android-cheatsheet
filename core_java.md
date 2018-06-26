# Core Java

### General

#### Implementing a Singleton
#### volatile
#### transient

#### Exceptions

### Data Structures

#### `Object` class and its methods

Object is a base class for all others. It has following methods:

* `hashCode` -- returns a hash value for the object. This value are used for finding the object in collections.
* `equals` -- returns if the object is equal to the argument object. Equal objects should have equal hash codes
* `toString` -- returns a string representation of an object. Usually is used in logging
* `wait`/`notify` -- implementing thread lock mechanism
* `finalize` -- called by garbage collector when the object is about to be collected

#### Collections

##### Arrays and Lists

Array is a set of items placed one after another in the memory. Elements of the array can be accessed fast because of memory organization, but it is impossible to add elements.

Arrays can contain objects or primitives. They have special syntax for creation and accessing elements:
```java
int arr[] = new int[10]
arr[2] = 199
```

A linked list is also a set of items, but it is organized in different way. Every item contains a value and links to the next and/or previous elements. Types of linked lists:

* Stack -- First-In-Last-Out list. New element is added to the head of the list.
* Queue -- First-In-First-Out list. New element is addede to the end of the list.
* Deque -- double-linked list, can work both ways.

Java has different implementations of lists. They differs by:

* Inner structure (may contain array or linked list for data storage)
* Thread safety
* 


Array classes are in fact wrappers on the fixed size array. The difference is following:

1. We can add items array classes objects, but not to fixed size array
1. Fixed size array can contain items of primitive or object types, whereas array classes objects can contain only objects

`Vector` is synchronized, so it shouldn't be used if thread safety is not needed.

##### Lists

Basic structures for lists:

The most common implementations is `LinkedList`.

##### Maps

##### Sets

##### Heap

##### Runtime Complexity
| List       | get  | addFirst | addLast | Remove | Inner Structure |
|:----------:|------|----------|---------|--------|-----------------|
| ArrayList  | O(1) | O(N)     | O(1) in general,  O(N) in the worst case    | O(N)   | Array |
| LinkedList | O(N) | O(1)     | O(N)    | O(N)   | Double-linked list |
| ArrayDeque | O(1) | O(N)     | O(1) in general, O(N) in the worst case    | O(N)   | Array |


### Multithreading

#### Wait/notify mechanism
#### Thread-safe collections

### References