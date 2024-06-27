# Java 8

# Collections
### Thread-Safe Data Structures:

1.  **Synchronized Collections (Legacy)**:
    
    -   `Vector`
    -   `Stack`
    -   `Hashtable`
2.  **Collections from `java.util.concurrent` package**:
    -   `ConcurrentHashMap`
    -   `CopyOnWriteArrayList`
    -   `CopyOnWriteArraySet`
    -   `ConcurrentLinkedQueue`
    -   `ConcurrentLinkedDeque`
    -   `LinkedBlockingQueue`
    -   `ArrayBlockingQueue`
    -   `PriorityBlockingQueue`
    -   `DelayQueue`
    -   `SynchronousQueue`
    -   `LinkedTransferQueue`
    -   `ConcurrentSkipListMap`
    -   `ConcurrentSkipListSet`
3.  **Synchronized Wrappers**: The `Collections` utility class provides methods to create synchronized versions of non-thread-safe collections.
    
    -   `Collections.synchronizedList(new ArrayList<>())`
    -   `Collections.synchronizedSet(new HashSet<>())`
    -   `Collections.synchronizedMap(new HashMap<>())`

### Not Thread-Safe Data Structures:

1.  **Standard Collections from `java.util` package**:
    -   `ArrayList`
    -   `LinkedList`
    -   `HashSet`
    -   `TreeSet`
    -   `HashMap`
    -   `TreeMap`
    -   `LinkedHashMap`
    -   `LinkedHashSet`

**Synchronized data structures**, like `Vector` and `Hashtable`, use coarse-grained locking to ensure thread safety by locking the entire structure for each operation. 
This approach can lead to significant performance overhead under high contention, as it prevents multiple threads from accessing the structure concurrently. 

**Concurrent data structures**, such as `ConcurrentHashMap` and `CopyOnWriteArrayList`, employ fine-grained locking or lock-free algorithms, allowing multiple threads to operate on the data structure simultaneously with minimal performance degradation. 
These concurrent collections are optimized for high-concurrency scenarios, providing better performance and scalability compared to their synchronized counterparts.


## Data Structures
 - Stack
1.  **Push**: Add an element to the top of the stack.
2.  **Pop**: Remove and return the element from the top of the stack.
3.  **Peek**: Return the element at the top of the stack without removing it.
4.  **isEmpty**: Check if the stack is empty.
5.  **Search**: Return the 1-based position of an element in the stack.

- Queue
 1. **addFirst**: The `addFirst(E e)` method inserts the specified element at the front of the deque. If the deque is full and cannot accommodate the additional element due to capacity restrictions (for example, in a bounded `Deque` implementation), `addFirst` will throw an `IllegalStateException`.
 2. **offerFirst**: The `offerFirst(E e)` method inserts the specified element at the front of the deque if it is possible to do so immediately without violating capacity restrictions. Else It'll return false;

> This class is likely to be faster than Stack when used as a stack, and
> faster than LinkedList when used as a queue. 

-   `ArrayList`  is resized to a new size of  `oldCapacity + (oldCapacity >> 1)`, resulting in an increse of ~50%. The default capacity is 10, resulting in a capacities after resize of 15, 22, 33, 49, 73, 109, 163, 244, 366...
    
-   `ArrayDeque`  is always resized to a power of 2. On resize, the capacity is doubled. Starting with the default of 16, the resuling capacities after resize are 32, 64, 128, 256,...


```java
Stack<Integer>  stack  =  new  Stack<>();
push(), pop(), peek()

Deque<Integer> deque = new ArrayDeque<>();
addFirst(E), addLast(E), 
offerFirst(E), offerLast(E), 

removeFirst(), removeLast(), 
pollFirst(), pollLast(), 

getFirst(), getLast(), 
peekFirst(), peekLast(), 

push(E), pop(),  // At First Location
offer(E), // Insert at First Location
poll(), // Remove at First Location
peek(), // Look at first but not remove
removeFirstOccurrence(Object), removeLastOccurrence(Object), descendingIterator()
```



# Java 17
**Java SE 8, 11, 17 and 21** are LTS releases

 - **Text Blocks**
 ```java
 private static void jsonBlock() {
    String text = """
            {
              "name": "John Doe",
              "age": 45,
              "address": "Doe Street, 23, Java Town"
            }
          """;
    System.out.println(text);
} 
``` 

- **Improved Switch Statements**
Java allows use of operator **_->(arrow)_** instead of **_: (colon)_** to denote the return expression. **_break_** keyword will not be needed when returning using switch in this expression, but **_default_** case is required.

```java
private static void improvedSwitch(Fruit fruit) {
    String text = switch (fruit) {
        case APPLE, PEAR -> {
            System.out.println("the given fruit was: " + fruit);
            yield "Common fruit";
        }
        case ORANGE, AVOCADO -> "Exotic fruit";
        default -> "Undefined fruit";
    };
    System.out.println(sql);
}```

### Summary

![alt text](https://raw.githubusercontent.com/anshulmajoka/interview-prep-notes/main/images/java8.jpg)

``` java
IntStream.concat(Arrays.stream(a), Arrays.stream(b)).sorted().toArray();
**three maximum numbers and three minimum numbers**
listOfIntegers.stream().sorted().limit(3).forEach(System.out::println);
listOfIntegers.stream().sorted(Comparator.reverseOrder()).limit(3).forEach(System.out::println);

**anagrams**
String s1 = "RaceCar";
String s2 = "CarRace";
s1 = Stream.of(s1.split(``""``)).map(String::toUpperCase).sorted().collect(Collectors.joining());
s2 = Stream.of(s2.split(``""``)).map(String::toUpperCase).sorted().collect(Collectors.joining());
```

```java
int i = 15623;
Integer sumOfDigits = Stream.of(String.valueOf(i).split("")).collect(Collectors.summingInt(Integer::parseInt));
  
List<String> listOfStrings = Arrays.asList("Java","Python","C#","HTML","Kotlin","C++","COBOL","C");
listOfStrings.stream().sorted(Comparator.comparing(String::length)).forEach(System.out::println);

int sum = Arrays.stream(a).sum();
double average = Arrays.stream(a).average().getAsDouble();        
```

``` java
.collect(Collectors.partitioningBy(i -> i % 2 == 0));
.stream().distinct().collect(Collectors.toList());
.mapToObj(c -> (char) c).collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));

**common elements between two arrays?**
`List<Integer> list1 = Arrays.asList(``71``,` `21``,` `34``,` `89``,` `56``,` `28``);`
`List<Integer> list2 = Arrays.asList(``12``,` `56``,` `17``,` `21``,` `94``,` `34``);`
`list1.stream().filter(list2::contains).forEach(System.out::println);`

**Reverse each word of a string using Java 8 streams?**
`String reversedStr = Arrays.stream(str.split(``" "``))`
`.map(word ->` `new` `StringBuffer(word).reverse())`
`.collect(Collectors.joining(``" "``));`

**Reverse an integer array**
`int``[] array =` `new` `int``[] {5,1,7,3,9,6};
`int``[] reversedArray = IntStream.rangeClosed(``1``, array.length).map(i -> array[array.length - i]).toArray();`

```

``` java

//frequency of each element in an array or a list
List<String> stationeryList = Arrays.asList("Pen", "Eraser", "Note Book", "Pen", "Pencil", "Stapler", "Note Book", "Pencil");        
Map<String, Long> stationeryCountMap = 
                stationeryList.stream().collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
```

``` java
decimalList.stream().sorted(Comparator.reverseOrder()).forEach(System.out::println);

//6) Given a list of strings, join the strings with ‘[‘ as prefix, ‘]’ as suffix and ‘,’ as delimiter?
String joinedString = listOfStrings.stream().collect(Collectors.joining(", ", "[", "]"));

int max = listOfIntegers.stream().max(Comparator.naturalOrder()).get();
int min = listOfIntegers.stream().min(Comparator.naturalOrder()).get();

```

``` java
//Merging Two Streams
Stream<Integer> resultingStream = Stream.concat(stream1, stream2);
Stream<Integer> resultingStream = Stream.of(
      stream1, stream2, stream3, stream4)
      .flatMap(i -> i);
-   We first create a new  _Stream_  containing the 4  _Streams,_  which results in a  _Stream<Stream<Integer>>_
-   Then we  _flatMap()_  this into a  _Stream<Integer>_  using the identity function

```

``` java
## Find the count of student in each department

Map<String, Long> countStudentInEachdept = list.stream()  
.collect(Collectors.groupingBy(Student::getDepartmantName, Collectors.counting()));  
System.out.println("Student count in each department : "+countStudentInEachdept);

```

``` java
## Find the average age of male and female students

Map<String, Double> mapAvgAge = list.stream()  
.collect(Collectors.groupingBy(Student::getGender, Collectors.averagingInt(Student::getAge)));  
System.out.println("Average age of male and female students : "+mapAvgAge);

**most repeated element in an array?**

`List<String> listOfStrings = Arrays.asList(``"Pen"``,` `"Eraser"``,` `"Note Book"``,` `"Pen"``,` `"Pencil"``,` `"Pen"``,` `"Note Book"``,` `"Pencil"``);`
`Map<String, Long> elementCountMap = listOfStrings.stream()`
`.collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));`

`Entry<String, Long> mostFrequentElement = elementCountMap.entrySet().stream().max(Map.Entry.comparingByValue()).get();`
```

``` java
**extract duplicate elements from an array?**
`List<Integer> listOfIntegers = Arrays.asList(``111``,` `222``,` `333``,` `111``,` `555``,` `333``,` `777``,` `222``);`

`Set<Integer> uniqueElements =` `new` `HashSet<>();`
`Set<Integer> duplicateElements = listOfIntegers.stream().filter(i -> ! uniqueElements.add(i)).collect(Collectors.toSet());` 
//[333, 222, 111]

**first repeated character in a string?**

Map<String, Long> charCountMap = Arrays.stream(inputString.split(""))
.collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()));`

String firstRepeatedChar = charCountMap.entrySet()
.stream()
.filter(entry -> entry.getValue() >1)
.map(entry -> entry.getKey())
.findFirst()
.get();

```
```java
**Fibonacci series**
Stream.iterate(new int[] {0,1}, f -> new int[] {f[1], f[0]+f[1]})`
.limit(10)
.map(f -> f[0])
.forEach(i -> System.out.print(i+ " "));
```
``` java
## Find the department who is having maximum number of students**
Entry<String, Long> entry = list.stream()  
.collect(Collectors.groupingBy(Student::getDepartmantName, Collectors.counting()))
.entrySet().stream()  
.max(Map.Entry.comparingByValue()).get();  
System.out.println("Department having maximum number of students : "+entry);

## - Find the Students who stays in Delhi and sort them by their names**
List<Student> lstDelhistudent = list.stream()
.filter(dt -> dt.getCity().equals("Delhi"))
.sorted(Comparator.comparing(Student::getFirstName))
.collect(Collectors.toList());  
System.out.println("List of students who stays in Delhi and sort them by their names : "+lstDelhistudent);

## - Find the average rank in all departments**
Map<String, Double> collect = list.stream()  
.collect(Collectors.groupingBy(Student::getDepartmantName, Collectors.averagingInt(Student::getRank)));  
System.out.println("Average rank in all departments : "+collect);

## - Find the highest rank in each department**
Map<String, Optional<Student>> studentData = list.stream().collect(Collectors.groupingBy(Student::getDepartmantName,  
Collectors.minBy(Comparator.comparing(Student::getRank))));  
System.out.println("Highest rank in each department : "+studentData);

## - Find the student who has second rank**
Student  student  = list.stream().sorted(Comparator.comparing(Student::getRank)).skip(1).findFirst().get();  
System.out.println("Second highest rank student : "+student);




```
# MultiThreading

## Key Concepts

### 1. **Thread Class and Runnable Interface**

-   **Thread Class**: You can create a new thread by extending the `Thread` class and overriding its `run` method.
- **Runnable Interface**: You can create a new thread by implementing the `Runnable` interface and passing an instance of your class to a `Thread` object.
- **Callable Interface**: You can create a new thread by implementing the `Callable` interface. The  _Callable_  interface is a generic interface containing a single  _call()_  method that returns a generic value .

*We can run _Runnable_ tasks using the _Thread_ class or _ExecutorService_, whereas we can only run _Callable_s using the latter.* 
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}
MyThread t = new MyThread();
t.start();
//------------------------------------------------
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread is running");
    }
}
MyRunnable myRunnable = new MyRunnable();
Thread t = new Thread(myRunnable);
t.start();

```
### 2. **Thread Lifecycle**

A thread in Java goes through several states in its lifecycle:

-   **New**: When a thread is created but not yet started.
-   **Runnable**: When a thread is ready to run and waiting for CPU time.
-   **Blocked**: When a thread is waiting for a monitor lock to enter a synchronized block/method.
-   **Waiting**: When a thread is waiting indefinitely for another thread to perform a particular action.
-   **Timed Waiting**: When a thread is waiting for another thread to perform an action for up to a specified waiting time.
-   **Terminated**: When a thread has completed its execution.

### 3. **Synchronization**

To prevent thread interference and memory consistency errors, synchronization is used:

-   **Synchronized Method**: Ensures that only one thread can execute a method at a time on the same object.
- **Synchronized Block**: Provides more granular control over the synchronization.
```java
synchronized void synchronizedMethod() {
    // critical section code
}

void method() {
    synchronized (this) {
        // critical section code
    }
}


```
### 4. **Inter-thread Communication**
Java provides methods like `wait()`, `notify()`, and `notifyAll()` for threads to communicate with each other.

-   **wait()**: Causes the current thread to wait until another thread invokes `notify()` or `notifyAll()` on the same object.
-   **notify()**: Wakes up a single thread that is waiting on the object's monitor.
-   **notifyAll()**: Wakes up all threads that are waiting on the object's monitor.

### Example 1: Producer-Consumer Problem
```java 
class SharedBuffer {
    private int data;
    private boolean empty = true;

    public synchronized void produce(int newData) throws InterruptedException {
        while (!empty) {
            wait();
        }
        data = newData;
        empty = false;
        System.out.println("Produced: " + newData);
        notify();
    }

    public synchronized int consume() throws InterruptedException {
        while (empty) {
            wait();
        }
        empty = true;
        System.out.println("Consumed: " + data);
        notify();
        return data;
    }
}

class Producer implements Runnable {
    private SharedBuffer buffer;

    public Producer(SharedBuffer buffer) {
        this.buffer = buffer;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            try {
                buffer.produce(i);
                Thread.sleep(100); // Simulate time taken to produce
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
    }
}

class Consumer implements Runnable {
    private SharedBuffer buffer;

    public Consumer(SharedBuffer buffer) {
        this.buffer = buffer;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            try {
                buffer.consume();
                Thread.sleep(150); // Simulate time taken to consume
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        SharedBuffer buffer = new SharedBuffer();
        Thread producerThread = new Thread(new Producer(buffer));
        Thread consumerThread = new Thread(new Consumer(buffer));
        
        producerThread.start();
        consumerThread.start();
    }
}

```
### Example 2: Using `notifyAll()`
Here, we modify the producer-consumer example to handle multiple consumers and producers using `notifyAll()`.
```java
class SharedBuffer {
    private int data;
    private boolean empty = true;

    public synchronized void produce(int newData) throws InterruptedException {
        while (!empty) {
            wait();
        }
        data = newData;
        empty = false;
        System.out.println("Produced: " + newData);
        notifyAll();
    }

    public synchronized int consume() throws InterruptedException {
        while (empty) {
            wait();
        }
        empty = true;
        System.out.println("Consumed: " + data);
        notifyAll();
        return data;
    }
}

class Producer implements Runnable {
    private SharedBuffer buffer;

    public Producer(SharedBuffer buffer) {
        this.buffer = buffer;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            try {
                buffer.produce(i);
                Thread.sleep(100); // Simulate time taken to produce
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
    }
}

class Consumer implements Runnable {
    private SharedBuffer buffer;

    public Consumer(SharedBuffer buffer) {
        this.buffer = buffer;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            try {
                buffer.consume();
                Thread.sleep(150); // Simulate time taken to consume
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        SharedBuffer buffer = new SharedBuffer();
        
        Thread producerThread1 = new Thread(new Producer(buffer));
        Thread producerThread2 = new Thread(new Producer(buffer));
        Thread consumerThread1 = new Thread(new Consumer(buffer));
        Thread consumerThread2 = new Thread(new Consumer(buffer));

        producerThread1.start();
        producerThread2.start();
        consumerThread1.start();
        consumerThread2.start();
    }
}

```

### 5. **Thread Pools**

### `Future`
Introduced in Java 5, Future interface represents the result of an asynchronous computation. It provides methods to check if the computation is complete, to wait for its completion, and to retrieve the result of the computation. Additionally, it allows the task to be canceled.

-   Key Methods:
    -   isDone(): Check if the task is complete.
    -   isCancelled(): Check if the task was canceled.
    -   cancel(boolean  mayInterruptIfRunning): Attempt to cancel the task.  
    -   get(): Wait and retrieve the result.    
    -   get(long timeout, TimeUnit unit): Wait with a timeout and retrieve the result.
        
**Usage**: Submit tasks to an ExecutorService and manage their execution and results asynchronously.
-   **Basics**: Represents a result of an asynchronous computation.
-   **Blocking**: Methods like `get()` block until the computation is complete.
-   **Cancellation**: Supports task cancellation.
-   **Limitations**: Cannot manually complete the result, no chaining, and lacks exception handling.

```Java
FutureExample.java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.TimeoutException;

class MyCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        Thread.sleep(2000); // Simulate some computation
        return "Result of Callable";
    }
}

public class FutureExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();
        
        Callable<String> callableTask = new MyCallable();
        Future<String> future = executor.submit(callableTask);
        
        try {
            // Wait for the result with a timeout of 1 second
            String result = future.get(1, TimeUnit.SECONDS);
            System.out.println("Result: " + result);
        } catch (TimeoutException e) {
            System.out.println("Timeout occurred while waiting for the result");
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
        
        // Check if the task is done
        if (!future.isDone()) {
            System.out.println("Task is not completed yet. Canceling the task...");
            future.cancel(true); // Cancel the task
        }
        
        // Check if the task was canceled
        if (future.isCancelled()) {
            System.out.println("Task was canceled");
        }
        
        executor.shutdown();
    }
}
```
### `CompletableFuture`

-   **Basics**: Extends `Future`, providing a more flexible and powerful API.
-   **Non-blocking**: Methods like `thenApply()`, `thenAccept()`, and `thenRun()` allow for non-blocking chaining of tasks.
-   **Manual Completion**: Can be manually completed using `complete()`.
-   **Combining Futures**: Allows combining multiple futures with methods like `thenCombine()`, `thenCompose()`, and `allOf()`.
-   **Exception Handling**: Provides methods for handling exceptions, like `exceptionally()` and `handle()`.

#### Key Differences with Future

 -   **Functionality**: `CompletableFuture` supports a richer set of features, including chaining, manual completion, and better exception handling.
 -   **Non-blocking**: `CompletableFuture` methods allow for non-blocking operations, whereas `Future` relies on blocking methods to retrieve results.
 -   **Combination and Composition**: `CompletableFuture` can combine multiple asynchronous tasks, enhancing the flexibility and power of concurrent programming in Java.

**Key Methods of CompletableFuture**

 - runAsync: Creates a new `CompletableFuture` that is asynchronously completed by a task running in the `ForkJoinPool.commonPool()` with a `Runnable`.
 - supplyAsync - Creates a new `CompletableFuture` that is asynchronously completed by a task running in the `ForkJoinPool.commonPool()` with a supplier.
 - thenApply - Returns a new `CompletableFuture` that is completed with the result of applying the given 		    function to the result of the current `CompletableFuture`.
 - thenAccept - Accepts the result of the computation asynchronously and returns `Void`.
 - thenCompose
 - thenCombine - Returns a new `CompletableFuture` that is completed with the result of combining the results of the current `CompletableFuture` and another `CompletableFuture` using the provided function.
 - exceptionally - Returns a new `CompletableFuture` that is completed with a result generated by the function if the original `CompletableFuture` completes exceptionally.
 - handle - Returns a new `CompletableFuture` that is completed when the current `CompletableFuture` completes, using the given function to compute the result or handle any exception.
 - 
 ```java
CompletableFuture<Void> future = CompletableFuture.runAsync(() -> {
    // Asynchronous task that doesn't return a value
    // Perform some computation
});

 CompletableFuture.supplyAsync(() -> {
    // Asynchronous computation
    return result;
});

CompletableFuture<Integer> future = CompletableFuture.supplyAsync(callableTask)
        .exceptionally(ex -> {
            System.err.println("Exception occurred: " + ex);
            return 0; // Default value or recovery logic
        });

int result = future.get(); // Handle exceptions during get() if not handled in exceptionally()


CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> 1);
CompletableFuture<String> chainedFuture = future.thenApply(result -> result.toString());

CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> 1);
CompletableFuture<Void> chainedFuture = future.thenAccept(result -> System.out.println("Result: " + result));

CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> 1);
CompletableFuture<String> chainedFuture = future.thenCompose(result -> CompletableFuture.completedFuture(result.toString()));

CompletableFuture<Integer> future1 = CompletableFuture.supplyAsync(() -> 1);
CompletableFuture<Integer> future2 = CompletableFuture.supplyAsync(() -> 2);
CompletableFuture<Integer> combinedFuture = future1.thenCombine(future2, (result1, result2) -> result1 + result2);

CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> {
    throw new RuntimeException("Exception occurred");
});
CompletableFuture<Integer> handledFuture = future.exceptionally(ex -> 0);

CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> {
    throw new RuntimeException("Exception occurred");
});
CompletableFuture<Integer> handledFuture = future.handle((result, ex) -> result != null ? result : 0);


```

These methods allow you to create, combine, and transform `CompletableFuture` instances, enabling powerful asynchronous programming in Java.

**Example: Asynchronous File Operation with runAsync() →** Imagine we have a Java application that needs to write a list of records to a file. Writing to a file can be time-consuming, especially if the data set is large. We want to perform this operation without stalling the main application flow.

```java
import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;
import java.io.IOException;

public class AsyncFileWritingExample {

    public static void main(String[] args) {
        List<String> dataToWrite = List.of("Line 1", "Line 2", "Line 3");

        CompletableFuture<Void> fileWritingFuture = CompletableFuture.runAsync(() -> {
            try {
                writeFile("example.txt", dataToWrite);
                System.out.println("File writing completed asynchronously: " + Thread.currentThread().getName());
            } catch (IOException e) {
                System.err.println("Error occurred while writing to the file: " + e.getMessage());
            }
        });

        // Continue with other operations
        System.out.println("Main thread is free to run other tasks.");

        // Optionally, wait for the file writing to complete
        try {
            fileWritingFuture.get(); // Blocks until the asynchronous file writing is complete
        } catch (Exception e) {
            e.printStackTrace();
        }

        System.out.println("All tasks completed.");
    }

    private static void writeFile(String fileName, List<String> data) throws IOException {
        Path path = Path.of(fileName);
        Files.write(path, data, StandardOpenOption.CREATE, StandardOpenOption.APPEND);
    }
}
```
