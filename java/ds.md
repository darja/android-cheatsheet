# Core Java. Data Structures

## `Object` class and its methods

Object is a base class for all others. It has following methods:

* `hashCode` — returns a hash value for the object. This value are used for finding the object in collections.
* `equals` — returns if the object is equal to the argument object. Equal objects should have equal hash codes
* `toString` — returns a string representation of an object. Usually is used in logging
* `wait`/`notify` — implementing thread lock mechanism
* `finalize` — called by garbage collector when the object is about to be collected

## Collections

### Arrays and Lists

#### Arrays in CS
Array is a set of items placed one after another in the memory. Elements of the array can be accessed fast because of memory organization, but it is impossible to add elements.

Arrays can contain objects or primitives. They have special syntax for creation and accessing elements:
```java
int arr[] = new int[10]
arr[2] = 199
```
#### Linked Lists in CS

A linked list is also a set of items, but it is organized in different way. Every item contains a value and links to the next and/or previous elements. Types of linked lists:

* Stack — Last-In-First-Out (LIFO) list. New element is added to the head of the list.
* Queue — First-In-First-Out (FIFO) list. New element is addede to the end of the list.
* Deque — double-linked list, can work both ways.

#### Lists in Java

Java has different implementations of lists. They differs by:

* Inner structure (may contain array or linked list for data storage) and, respectively, runtime complexity
* Thread safety. Also thread-safe collections can use synchronization or not.

##### Thread-safe lists without synchronization:
|                        | Add  | Remove | Get  | Contains | Next | Data Structure |
|------------------------|------|--------|------|----------|------|---------------|
| ConcurrentLinkedQueue  | O(1) | O(1) | O(1) | O(n) | O(n) | Linked List |
| CopyOnWriteArrayList   | O(n) | O(n) | O(1) | O(n) | O(1) | Array |

##### Thread-safe lists with synchronization:
|                        | Add  | Remove | Get  | Contains | Next | Data Structure |
|------------------------|------|--------|------|----------|------|---------------|
| Vector                 | O(1) or O(N) |  O(n)  | O(1) |   O(n)   | O(1) | Array |
| Stack                  | O(1) or O(N) |  O(n)  | O(1) |   O(n)   | O(1) | Array |

##### Thread-unsafe lists:
|                      | Add          | Remove | Get  | Contains | Next | Data Structure |
|----------------------|--------------|--------|------|----------|------|----------------|
| ArrayList            | O(1)         |  O(n)  | O(1) |   O(n)   | O(1) | Array          |
| LinkedList           | O(1)         |  O(1)  | O(n) |   O(n)   | O(1) | Linked List    |
| ArrayDequeue         | O(1) or O(N) |  O(1   | O(1) |  O(n)    | O(1) | Array          |

#### Maps

Map is a structure, that contains keys and one value for every key. The special structure allows to find a value for provided key for linear time.

Java implementations for maps:

* `HashMap` — basic implementation
* `Hashtable` — synchronized version, doesn't allow nulls
* `LinkedHashMap` — same as `HashMap`, but also maintains keys order
* `TreeMap` — keys are stored in red-black tree
* `ConcurrentHashMap` — thread-safe hash map

#### Sets

Set is a collection that guarantees that every element is stored only once.

Java implementations for sets:

* `HashSet` — based on `HashMap`
* `TreeSet` — based on `TreeMap`

#### Heap

**TODO: Move to CS section**

Heap is a tree-based data structure where root elements are greater or equal (max-heap) or smaller or equal (min-heap) than child elements.