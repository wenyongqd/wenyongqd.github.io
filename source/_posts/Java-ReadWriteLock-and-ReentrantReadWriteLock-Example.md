---
title: Java ReadWriteLock and ReentrantReadWriteLock Example
date: 2020-07-31 18:02:47
tags:
---

In this Java concurrency tutorial, you will understand how **ReadWriteLock** works and use it for simple cases with **ReentrantReadWriteLock** implementation.
Basically, a `ReadWriteLock` is designed as a high-level locking mechanism that allows you to add thread-safety feature to a data structure while increasing throughput by allowing multiple threads to read the data concurrently and one thread to update the data exclusively.
`ReadWriteLock` is an interface defined in the `java.util.concurrent.locks` package, with `ReentrantReadWriteLock` is an implementation class. So you can create a `ReadWriteLock` like this:
```java
ReadWriteLock rwLock = new ReentrantReadWriteLock();
```
The ReentrantReadWriteLock maintains two separate locks, one for reading and one for writing:
```java
Lock readLock = rwLock.readLock();
Lock writeLock = rwLock.writeLock();
```

Then you can use the read lock to safeguard a code block that performs read operation like this:
```java
readLock.lock();
 
try {
    // reading data
} finally {
 
    readLock.unlock();
}
```
And use the write lock to safeguard a code block that performs update operation like this:

```java
writeLock.lock();
 
try {
    // update data
} finally {
 
    writeLock.unlock();
}
```

A `ReadWriteLock` implementation guarantees the following behaviors:
* Multiple threads can read the data at the same time, as long as there’s no thread is updating the data.
* Only one thread can update the data at a time, causing other threads (both readers and writers) block until the write lock is released.
* If a thread attempts to update the data while other threads are reading, the write thread also blocks until the read lock is released.

So `ReadWriteLock` can be used to add concurrency features to a data structure, but it doesn’t guarantee the performance because it depends on various factors: how the data structure is designed, the contention of reader and writer threads at real time, CPU architecture (single core  or multicores), etc.
Similar to `ReentrantLock`, the `ReentrantReadWriteLock` allows a thread to acquire the read lock or write lock multiple times recursively, thus the word “Reentrant”.

Let’s see an example that adds concurrency features to an ArrayList using ReentrantReadWriteLock. Consider the following data structure:

```java
import java.util.*;
import java.util.concurrent.locks.*;
 
/**
 * ReadWriteList.java
 * This class demonstrates how to use ReadWriteLock to add concurrency
 * features to a non-threadsafe collection
 * @author www.codejava.net
 */
public class ReadWriteList<E> {
    private List<E> list = new ArrayList<>();
    private ReadWriteLock rwLock = new ReentrantReadWriteLock();
 
    public ReadWriteList(E... initialElements) {
        list.addAll(Arrays.asList(initialElements));
    }
 
    public void add(E element) {
        Lock writeLock = rwLock.writeLock();
        writeLock.lock();
 
        try {
            list.add(element);
        } finally {
            writeLock.unlock();
        }
    }
 
    public E get(int index) {
        Lock readLock = rwLock.readLock();
        readLock.lock();
 
        try {
            return list.get(index);
        } finally {
            readLock.unlock();
        }
    }
 
    public int size() {
        Lock readLock = rwLock.readLock();
        readLock.lock();
 
        try {
            return list.size();
        } finally {
            readLock.unlock();
        }
    }
 
}
```

As you can see, this class wraps an `ArrayList` as the underlying data structure. It uses the read lock to safeguard concurrent access to the read operations (`get()` and `size()` methods) and uses the write lock to safeguard concurrent access to the write operations (`add()` method).
Next, create a writer thread that randomly adds a number to the shared list. Here’s the code:

```java
import java.util.*;
 
/**
 * Writer.java
 * This thread randomly read an element from a shared data structure
 * @author www.codejava.net
 */
public class Writer extends Thread {
    private ReadWriteList<Integer> sharedList;
 
    public Writer(ReadWriteList<Integer> sharedList) {
        this.sharedList = sharedList;
    }
 
    public void run() {
        Random random = new Random();
        int number = random.nextInt(100);
        sharedList.add(number);
 
        try {
            Thread.sleep(100);
            System.out.println(getName() + " -> put: " + number);
        } catch (InterruptedException ie ) { ie.printStackTrace(); }
    }
}
```

Also create a reader thread that randomly gets an element from the shared list. Here’s the code:

```java
import java.util.*;
 
/**
 * Reader.java
 * This thread randomly adds an element to a shared data structure
 * @author www.codejava.net
 */
public class Reader extends Thread {
    private ReadWriteList<Integer> sharedList;
 
    public Reader(ReadWriteList<Integer> sharedList) {
        this.sharedList = sharedList;
    }
 
    public void run() {
        Random random = new Random();
        int index = random.nextInt(sharedList.size());
        Integer number = sharedList.get(index);
 
        System.out.println(getName() + " -> get: " + number);
 
        try {
            Thread.sleep(100);
        } catch (InterruptedException ie ) { ie.printStackTrace(); }
 
    }
}
```

Now, let’s create a test program like the following:

```java
import java.util.*;
 
/**
 * ReadWriteLockTest.java
 * Test program for understanding ReadWriteLock
 * @author www.codejava.net
 */
public class ReadWriteLockTest {
    static final int READER_SIZE = 10;
    static final int WRITER_SIZE = 2;
 
    public static void main(String[] args) {
        Integer[] initialElements = {33, 28, 86, 99};
 
        ReadWriteList<Integer> sharedList = new ReadWriteList<>(initialElements);
 
        for (int i = 0; i < WRITER_SIZE; i++) {
            new Writer(sharedList).start();
        }
 
        for (int i = 0; i < READER_SIZE; i++) {
            new Reader(sharedList).start();
        }
 
    }
}
```

As you can see, this program creates and runs 10 reader threads and 2 writer threads that work on a shared `ReadWriteList` data structure. Compile and run the program to observe the output.
If you consult the Javadoc you will see that it is more sophisticated with fairness policy and other locking methods, so read more about it when you have time.

To conclude, remember the following key points:
* `ReadWriteLock` allows multiple concurrent readers abut only one exclusive writer.
* `ReentrantReadWriteLock` is an implementation of `ReadWriteLock`. In addition, it allows a reader/writer thread acquire a read lock/write lock multiple times recursively (reentrancy).
* Use the read lock to safeguard code that performs read operations, and use the write lock to protect access to code that performs update operation.
* In practice, `ReadWriteLock` can be used to increase throughput for shared data structure like cache or dictionary-like data which the update is infrequent and read is more frequent.