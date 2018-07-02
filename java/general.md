# Core Java. General

### Implementing a Singleton

```java
public class DclSingleton {
    private static volatile DclSingleton instance;
    public static DclSingleton getInstance() {
        if (instance == null) {
            synchronized (DclSingleton .class) {
                if (instance == null) {
                    instance = new DclSingleton();
                }
            }
        }
        return instance;
    }
    …
}
```

### volatile
`volatile` modifier for a variable means that all threads will modify this variable, but not copied instances.

### transient
`transient` modifier is used to indicate that a field should not be serialized.

### Exceptions
An exception is an event meaning that something went wrong in the code.

Java has special syntax for catching exceptions:

```java
try {
    // some code
} catch (Exception e) {
    // handle what happened
} finally {
    // do something after code is finished or exception is handled
}
```

Exceptions can be checked and unchecked. Checked exceptions are required to be handled in code with try-catch block, that is checked in compile-time. Unchecked (or runtime) exceptions don't have such requirement.

In Kotlin all exceptions are unchechecked.
