# UNIT 6: Exploring Java Language

---

## 1. Simple Type Wrappers (Exam Important ⭐)

### 1.1 What are Wrapper Classes?

**Wrapper classes** convert **primitive types** into **objects**. Each primitive type has a corresponding wrapper class in `java.lang`.

### 1.2 Primitive → Wrapper Mapping

| Primitive | Wrapper Class | Example |
|-----------|---------------|---------|
| `byte` | `Byte` | `Byte b = 10;` |
| `short` | `Short` | `Short s = 20;` |
| `int` | `Integer` | `Integer i = 30;` |
| `long` | `Long` | `Long l = 40L;` |
| `float` | `Float` | `Float f = 1.5f;` |
| `double` | `Double` | `Double d = 2.5;` |
| `char` | `Character` | `Character c = 'A';` |
| `boolean` | `Boolean` | `Boolean flag = true;` |

### 1.3 Autoboxing and Unboxing

```java
// Autoboxing: primitive → Object (automatic)
int a = 10;
Integer obj = a;          // Autoboxing
// Equivalent to: Integer obj = Integer.valueOf(a);

// Unboxing: Object → primitive (automatic)
Integer obj2 = new Integer(20);
int b = obj2;             // Unboxing
// Equivalent to: int b = obj2.intValue();
```

### 1.4 Useful Wrapper Methods

```java
// Parsing strings to primitives
int x = Integer.parseInt("123");
double y = Double.parseDouble("3.14");
boolean z = Boolean.parseBoolean("true");

// Primitives to string
String s1 = Integer.toString(42);
String s2 = String.valueOf(3.14);

// Constants
System.out.println(Integer.MAX_VALUE);  // 2147483647
System.out.println(Integer.MIN_VALUE);  // -2147483648
System.out.println(Double.MAX_VALUE);   // 1.7976931348623157E308

// Comparisons
int result = Integer.compare(10, 20);  // -1 (10 < 20)

// Type conversions
int i = Integer.valueOf("FF", 16);  // 255 (hex to int)
String binary = Integer.toBinaryString(10);  // "1010"
String hex = Integer.toHexString(255);       // "ff"
String octal = Integer.toOctalString(8);     // "10"
```

### 1.5 Why Wrapper Classes are Needed

1. **Collections** only work with objects, not primitives (`ArrayList<Integer>`)
2. **Null values** — primitives can't be null, but wrapper objects can
3. **Utility methods** — parseInt(), toString(), compareTo(), etc.
4. **Generics** require object types (`List<int>` ✗, `List<Integer>` ✓)
5. **Serialization** — objects can be serialized

---

## 2. Runtime Memory Management

### 2.1 Java Memory Areas

```
┌──────────────────────────────────────────────┐
│              JVM Memory                      │
│                                              │
│  ┌──────────────┐  ┌──────────────────────┐  │
│  │    STACK     │  │        HEAP           │  │
│  │              │  │                       │  │
│  │ Local vars   │  │  ┌──────────────────┐ │  │
│  │ Method calls │  │  │  Young Generation│ │  │
│  │ References   │  │  │  ┌────┐ ┌──────┐ │ │  │
│  │              │  │  │  │Eden│ │Surviv│ │ │  │
│  │ ┌──────────┐ │  │  │  └────┘ └──────┘ │ │  │
│  │ │ Frame 3  │ │  │  ├──────────────────┤ │  │
│  │ │ Frame 2  │ │  │  │  Old Generation  │ │  │
│  │ │ Frame 1  │ │  │  │  (Tenured)       │ │  │
│  │ │ main()   │ │  │  └──────────────────┘ │  │
│  │ └──────────┘ │  │                       │  │
│  └──────────────┘  └──────────────────────┘  │
│                                              │
│  ┌──────────────┐  ┌──────────────────────┐  │
│  │  Method Area │  │   String Pool        │  │
│  │ Class data   │  │   "Hello" "World"    │  │
│  │ Static vars  │  │                      │  │
│  └──────────────┘  └──────────────────────┘  │
└──────────────────────────────────────────────┘
```

### 2.2 Memory Areas Explained

| Area | Stores | Lifetime |
|------|--------|----------|
| **Stack** | Local variables, method calls, references | Per thread; freed when method returns |
| **Heap** | Objects, instance variables | Shared; freed by Garbage Collector |
| **Method Area** | Class metadata, static variables, bytecode | Until class is unloaded |
| **String Pool** | String literals | Shared; part of heap |
| **PC Register** | Current instruction of each thread | Per thread |
| **Native Stack** | Native (C/C++) method calls | Per thread |

### 2.3 Garbage Collection (Exam Important ⭐)

**Garbage Collection (GC)** is the automatic process of **reclaiming memory** occupied by objects that are no longer referenced.

```java
class GCDemo {
    public static void main(String[] args) {
        // Object created on heap
        Student s1 = new Student("Rahul");
        Student s2 = new Student("Priya");
        
        s1 = null;  // Object "Rahul" is now eligible for GC
        s2 = s1;    // Object "Priya" is now eligible for GC
        
        // Request GC (not guaranteed to run immediately)
        System.gc();
        // or
        Runtime.getRuntime().gc();
    }
    
    // Called before object is garbage collected
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Object is being garbage collected");
        super.finalize();
    }
}
```

### 2.4 Runtime Class

The `Runtime` class provides access to the JVM's runtime environment.

```java
public class RuntimeDemo {
    public static void main(String[] args) {
        Runtime runtime = Runtime.getRuntime();
        
        // Memory information
        System.out.println("Total Memory: " + runtime.totalMemory() / 1024 + " KB");
        System.out.println("Free Memory:  " + runtime.freeMemory() / 1024 + " KB");
        System.out.println("Max Memory:   " + runtime.maxMemory() / 1024 + " KB");
        System.out.println("Used Memory:  " + 
            (runtime.totalMemory() - runtime.freeMemory()) / 1024 + " KB");
        
        // Available processors
        System.out.println("Processors: " + runtime.availableProcessors());
        
        // Suggest garbage collection
        runtime.gc();
        System.out.println("After GC - Free: " + runtime.freeMemory() / 1024 + " KB");
        
        // Execute external commands
        try {
            Process p = runtime.exec("notepad.exe");
        } catch (Exception e) {
            System.out.println("Command failed: " + e.getMessage());
        }
    }
}
```

### 2.5 Key Points about GC

| Point | Description |
|-------|-------------|
| **Automatic** | JVM handles memory deallocation |
| **Non-deterministic** | Cannot predict exactly when GC will run |
| `System.gc()` | Only a **request**, not guaranteed |
| `finalize()` | Called before GC reclaims the object (deprecated in Java 9+) |
| **Eligibility** | Object with no live references is eligible |
| **GC Algorithms** | Serial, Parallel, CMS, G1, ZGC |

---

## 3. Object Cloning — clone() and Cloneable Interface (Exam Important ⭐)

### 3.1 What is Cloning?

**Cloning** creates an **exact copy** of an existing object. Java provides the `clone()` method (in `Object` class) and the `Cloneable` interface.

### 3.2 Steps to Clone an Object

```
Step 1: Implement the Cloneable interface (marker interface)
Step 2: Override the clone() method from Object class
Step 3: Call super.clone() inside clone()
Step 4: Handle CloneNotSupportedException
```

### 3.3 Shallow Clone

A **shallow clone** copies the object but shares the **same references** to nested objects.

```java
class Address {
    String city;
    String state;
    
    Address(String city, String state) {
        this.city = city;
        this.state = state;
    }
    
    @Override
    public String toString() {
        return city + ", " + state;
    }
}

class Student implements Cloneable {
    String name;
    int age;
    Address address;  // Reference type
    
    Student(String name, int age, Address address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }
    
    // Shallow Clone
    @Override
    public Object clone() throws CloneNotSupportedException {
        return super.clone();  // Default shallow clone
    }
    
    @Override
    public String toString() {
        return name + " (" + age + ") - " + address;
    }
}

public class ShallowCloneDemo {
    public static void main(String[] args) throws CloneNotSupportedException {
        Address addr = new Address("Mumbai", "Maharashtra");
        Student original = new Student("Rahul", 20, addr);
        
        Student clone = (Student) original.clone();
        
        System.out.println("Original: " + original);  // Rahul (20) - Mumbai, Maharashtra
        System.out.println("Clone:    " + clone);      // Rahul (20) - Mumbai, Maharashtra
        
        // Modifying clone's address affects original! (shared reference)
        clone.address.city = "Delhi";
        clone.name = "Amit";  // String is immutable, so this is safe
        
        System.out.println("\nAfter modifying clone:");
        System.out.println("Original: " + original);  // Rahul (20) - Delhi, Maharashtra ← CHANGED!
        System.out.println("Clone:    " + clone);      // Amit (20) - Delhi, Maharashtra
    }
}
```

```
Shallow Clone Memory:
                        Heap
original ──→ ┌──────────────┐
             │ name = "Rahul"│
             │ age = 20      │
             │ address ──────┼──→ ┌────────────────┐
             └──────────────┘    │ city = "Mumbai" │
                                  │ state = "MH"    │
clone ────→  ┌──────────────┐    │                  │
             │ name = "Rahul"│    └────────────────┘
             │ age = 20      │         ↑
             │ address ──────┼─────────┘ SHARED!
             └──────────────┘
```

### 3.4 Deep Clone

A **deep clone** copies the object AND creates **new copies** of all nested objects.

```java
class Student implements Cloneable {
    String name;
    int age;
    Address address;
    
    Student(String name, int age, Address address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }
    
    // Deep Clone
    @Override
    public Object clone() throws CloneNotSupportedException {
        Student cloned = (Student) super.clone();
        // Create new copy of Address
        cloned.address = new Address(this.address.city, this.address.state);
        return cloned;
    }
}

// Now modifying clone's address does NOT affect original
```

```
Deep Clone Memory:
                        Heap
original ──→ ┌──────────────┐
             │ name = "Rahul"│
             │ age = 20      │       ┌────────────────┐
             │ address ──────┼──→    │ city = "Mumbai" │
             └──────────────┘       │ state = "MH"    │
                                     └────────────────┘

clone ────→  ┌──────────────┐       ┌────────────────┐
             │ name = "Rahul"│       │ city = "Mumbai" │ ← SEPARATE COPY!
             │ age = 20      │       │ state = "MH"    │
             │ address ──────┼──→    └────────────────┘
             └──────────────┘
```

### 3.5 Shallow vs Deep Clone

| Feature | Shallow Clone | Deep Clone |
|---------|---------------|------------|
| **Nested objects** | Shared references | New copies |
| **Speed** | Faster | Slower |
| **Complexity** | Simple | Complex |
| **Independence** | Changes affect both | Fully independent |
| **Default in Java** | Yes (`super.clone()`) | Must implement manually |

---

## 4. Thread, ThreadGroup, and Runnable

### 4.1 Thread Class — Key Methods

| Method | Description |
|--------|-------------|
| `start()` | Starts the thread (calls run()) |
| `run()` | Contains the code to execute |
| `sleep(long ms)` | Pauses thread for ms milliseconds |
| `join()` | Waits for this thread to finish |
| `isAlive()` | Returns true if thread is running |
| `getName()` / `setName()` | Get/set thread name |
| `getPriority()` / `setPriority()` | Get/set priority |
| `interrupt()` | Interrupts a sleeping/waiting thread |
| `yield()` | Suggests giving up CPU to other threads |
| `currentThread()` | Returns reference to current thread |
| `isDaemon()` / `setDaemon()` | Check/set daemon thread |

### 4.2 Runnable Interface

The **Runnable** interface has a single method `run()`. It is the **preferred way** to create threads.

```java
// Using Runnable
class MyTask implements Runnable {
    private String taskName;
    
    MyTask(String name) {
        this.taskName = name;
    }
    
    @Override
    public void run() {
        for (int i = 1; i <= 3; i++) {
            System.out.println(taskName + " - Step " + i);
            try { Thread.sleep(500); } catch (InterruptedException e) {}
        }
        System.out.println(taskName + " completed");
    }
}

public class RunnableDemo {
    public static void main(String[] args) {
        // Create threads with Runnable
        Thread t1 = new Thread(new MyTask("Download"), "Download-Thread");
        Thread t2 = new Thread(new MyTask("Upload"), "Upload-Thread");
        Thread t3 = new Thread(new MyTask("Process"), "Process-Thread");
        
        t1.start();
        t2.start();
        t3.start();
        
        // Using Lambda (Java 8+)
        Thread t4 = new Thread(() -> {
            System.out.println("Lambda thread: " + Thread.currentThread().getName());
        }, "Lambda-Thread");
        t4.start();
    }
}
```

### 4.3 ThreadGroup (Exam Important ⭐)

A **ThreadGroup** is a collection of threads that can be managed as a single unit.

```
ThreadGroup Hierarchy:
┌──────────────────────┐
│   main (ThreadGroup)  │
│   ├── main (Thread)   │
│   ├── Group-A         │
│   │   ├── Thread-A1   │
│   │   └── Thread-A2   │
│   └── Group-B         │
│       ├── Thread-B1   │
│       └── Thread-B2   │
└──────────────────────┘
```

```java
public class ThreadGroupDemo {
    public static void main(String[] args) {
        // Create thread groups
        ThreadGroup groupA = new ThreadGroup("Download-Group");
        ThreadGroup groupB = new ThreadGroup("Upload-Group");
        
        // Create threads in groups
        Thread t1 = new Thread(groupA, () -> {
            for (int i = 0; i < 3; i++) {
                System.out.println(Thread.currentThread().getName() + ": " + i);
                try { Thread.sleep(500); } catch (InterruptedException e) {}
            }
        }, "Download-1");
        
        Thread t2 = new Thread(groupA, () -> {
            for (int i = 0; i < 3; i++) {
                System.out.println(Thread.currentThread().getName() + ": " + i);
                try { Thread.sleep(500); } catch (InterruptedException e) {}
            }
        }, "Download-2");
        
        Thread t3 = new Thread(groupB, () -> {
            for (int i = 0; i < 3; i++) {
                System.out.println(Thread.currentThread().getName() + ": " + i);
                try { Thread.sleep(500); } catch (InterruptedException e) {}
            }
        }, "Upload-1");
        
        t1.start();
        t2.start();
        t3.start();
        
        // ThreadGroup methods
        System.out.println("Group A name: " + groupA.getName());
        System.out.println("Active threads in A: " + groupA.activeCount());
        System.out.println("Active threads in B: " + groupB.activeCount());
        
        // List all threads in group
        groupA.list();  // Prints thread hierarchy
        
        // Set max priority for group
        groupA.setMaxPriority(Thread.NORM_PRIORITY);
        
        // Interrupt all threads in group
        // groupA.interrupt();
    }
}
```

### 4.4 ThreadGroup Key Methods

| Method | Description |
|--------|-------------|
| `getName()` | Returns group name |
| `getParent()` | Returns parent group |
| `activeCount()` | Number of active threads in group |
| `activeGroupCount()` | Number of active sub-groups |
| `list()` | Prints thread group hierarchy |
| `setMaxPriority(int)` | Sets max priority for group |
| `interrupt()` | Interrupts all threads in group |
| `enumerate(Thread[])` | Copies active threads to array |
| `destroy()` | Destroys the (empty) thread group |

### 4.5 Daemon Threads

**Daemon threads** are background threads that automatically terminate when all user (non-daemon) threads finish.

```java
public class DaemonDemo {
    public static void main(String[] args) {
        Thread daemon = new Thread(() -> {
            while (true) {
                System.out.println("Daemon thread running...");
                try { Thread.sleep(1000); } catch (InterruptedException e) {}
            }
        });
        
        daemon.setDaemon(true);  // MUST set before start()
        daemon.start();
        
        System.out.println("Main thread finishing...");
        // When main ends, daemon thread is automatically killed
    }
}
```

| Feature | User Thread | Daemon Thread |
|---------|-------------|---------------|
| **Purpose** | Main program tasks | Background services (GC, monitoring) |
| **JVM exit** | JVM waits for all user threads | JVM does NOT wait for daemons |
| **Example** | main thread | Garbage Collector |
| **Set daemon** | Default | `setDaemon(true)` before `start()` |

### 4.6 Thread vs Runnable — Complete Comparison

| Feature | Thread (class) | Runnable (interface) |
|---------|---------------|---------------------|
| **Extends/Implements** | `extends Thread` | `implements Runnable` |
| **Multiple inheritance** | Can't extend other class | Can extend another class |
| **Code reuse** | Less flexible | More flexible |
| **Object sharing** | Separate objects | Single Runnable, multiple threads |
| **Overhead** | Creates Thread object | Lightweight |
| **Preferred** | No | Yes ✓ |

```java
// Runnable allows extending another class
class MyTask extends SomeOtherClass implements Runnable {
    @Override
    public void run() {
        // Can extend SomeOtherClass AND be a thread task
    }
}

// Sharing same Runnable
Runnable task = new MyTask();
Thread t1 = new Thread(task);  // Share same task object
Thread t2 = new Thread(task);  // Both threads run same task
```

---

## 5. Important Exam Questions

### Short Answer Questions
1. What are wrapper classes? List all 8 wrapper classes.
2. What is the difference between shallow clone and deep clone?
3. What is a ThreadGroup? List its methods.
4. Differentiate between Thread class and Runnable interface.

### Long Answer Questions
1. Explain object cloning in Java. Differentiate between shallow and deep cloning with code examples.
2. Explain Java Runtime Memory Management. What is Garbage Collection? How does it work?
3. What are Wrapper classes? Explain autoboxing and unboxing with examples.
4. Explain ThreadGroup with example. How are daemon threads different from user threads?
