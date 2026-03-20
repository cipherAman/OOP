# UNIT 4: Multithreading, String Handling, Java I/O, JDBC & Networking

---

## PART A: MULTITHREADING

---

## 1. Java Thread Model

### 1.1 What is a Thread?

A **thread** is the **smallest unit of execution** within a process. A process can have multiple threads that execute concurrently.

```
Process (Java Application)
┌──────────────────────────────────────┐
│                                      │
│  ┌──────────┐ ┌──────────┐ ┌──────┐ │
│  │ Thread 1 │ │ Thread 2 │ │Thread│ │
│  │ (main)   │ │ (worker) │ │  3   │ │
│  └──────────┘ └──────────┘ └──────┘ │
│                                      │
│  Shared Memory (Heap)                │
│  ┌──────────────────────────────┐    │
│  │ Objects, static variables    │    │
│  └──────────────────────────────┘    │
└──────────────────────────────────────┘
```

### 1.2 Multithreading vs Multiprocessing

| Feature | Multithreading | Multiprocessing |
|---------|---------------|-----------------|
| Basic Unit | Thread | Process |
| Memory | Shared memory | Separate memory |
| Switching | Faster (lightweight) | Slower (heavy) |
| Communication | Easy (shared memory) | Complex (IPC) |
| Resource | Less resource intensive | More resource intensive |

### 1.3 Thread Life Cycle (Exam Important ⭐)

```
                    ┌─────────┐
          start()   │   NEW   │  (Thread created)
          ┌────────→│         │
          │         └────┬────┘
          │              │ start()
          │              ↓
          │         ┌─────────┐
          │         │RUNNABLE │  (Ready to run / Running)
          │         │         │←──────────────────┐
          │         └────┬────┘                   │
          │          ┌───┼───┐                    │
          │          ↓   ↓   ↓                    │
    ┌──────────┐  ┌────────────┐  ┌────────────┐ │
    │ BLOCKED  │  │  WAITING   │  │   TIMED    │ │
    │(lock)    │  │ (wait())   │  │  WAITING   │ │
    │          │  │ (join())   │  │ (sleep())  │ │
    └────┬─────┘  └─────┬──────┘  └─────┬──────┘ │
         │              │               │         │
         └──────────────┴───────────────┘─────────┘
                              │ (notify/timeout/lock acquired)
                              ↓
                    ┌─────────────────┐
                    │   TERMINATED    │  (run() completes)
                    │   (DEAD)        │
                    └─────────────────┘
```

### 1.4 Thread States

| State | Description |
|-------|-------------|
| **NEW** | Thread object created, `start()` not yet called |
| **RUNNABLE** | Thread ready to run; may or may not be running |
| **BLOCKED** | Waiting to acquire a lock/monitor |
| **WAITING** | Waiting indefinitely for another thread (wait(), join()) |
| **TIMED_WAITING** | Waiting for a specified time (sleep(), wait(ms)) |
| **TERMINATED** | Thread has finished execution |

---

## 2. Thread Priorities

### 2.1 Priority Constants

| Constant | Value | Description |
|----------|-------|-------------|
| `Thread.MIN_PRIORITY` | 1 | Lowest priority |
| `Thread.NORM_PRIORITY` | 5 | Default priority |
| `Thread.MAX_PRIORITY` | 10 | Highest priority |

### 2.2 Using Priorities

```java
class MyThread extends Thread {
    public MyThread(String name) {
        super(name);
    }
    
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(getName() + " (Priority: " + getPriority() + "): " + i);
        }
    }
}

public class PriorityDemo {
    public static void main(String[] args) {
        MyThread t1 = new MyThread("Low");
        MyThread t2 = new MyThread("Normal");
        MyThread t3 = new MyThread("High");
        
        t1.setPriority(Thread.MIN_PRIORITY);    // 1
        t2.setPriority(Thread.NORM_PRIORITY);   // 5
        t3.setPriority(Thread.MAX_PRIORITY);    // 10
        
        t1.start();
        t2.start();
        t3.start();
    }
}
```

> **Note:** Thread priority is a **hint** to the thread scheduler. The OS may or may not honor it.

---

## 3. Synchronization (Exam Important ⭐)

### 3.1 What is Synchronization?

Synchronization controls **access to shared resources** by multiple threads to prevent **data inconsistency** and **race conditions**.

### 3.2 The Problem (Without Synchronization)

```java
// Shared resource - NOT thread-safe
class Counter {
    int count = 0;
    
    void increment() {
        count++;  // NOT atomic: read → modify → write
    }
}
// Two threads incrementing simultaneously can cause lost updates
```

### 3.3 Synchronized Method

```java
class Counter {
    int count = 0;
    
    // Only ONE thread can execute this method at a time
    synchronized void increment() {
        count++;
    }
    
    synchronized int getCount() {
        return count;
    }
}
```

### 3.4 Synchronized Block

```java
class Counter {
    int count = 0;
    
    void increment() {
        // Only this block is synchronized — more efficient
        synchronized (this) {
            count++;
        }
    }
}
```

### 3.5 Complete Example

```java
class BankAccount {
    private int balance = 1000;
    
    synchronized void withdraw(int amount) {
        if (balance >= amount) {
            System.out.println(Thread.currentThread().getName() + 
                             " withdrawing: " + amount);
            try { Thread.sleep(100); } catch (InterruptedException e) {}
            balance -= amount;
            System.out.println(Thread.currentThread().getName() + 
                             " Balance: " + balance);
        } else {
            System.out.println("Insufficient balance for " + 
                             Thread.currentThread().getName());
        }
    }
}

public class SyncDemo {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount();
        
        Thread t1 = new Thread(() -> acc.withdraw(800), "Thread-1");
        Thread t2 = new Thread(() -> acc.withdraw(800), "Thread-2");
        
        t1.start();
        t2.start();
    }
}
/* With synchronization:
   Thread-1 withdrawing: 800
   Thread-1 Balance: 200
   Insufficient balance for Thread-2
*/
```

---

## 4. Creating a Thread

### 4.1 Two Ways to Create Threads

```
Way 1: Extending Thread class
┌────────────────────┐
│   Thread (class)   │
└────────┬───────────┘
         ↓ extends
┌────────────────────┐
│   MyThread         │
│   (override run()) │
└────────────────────┘

Way 2: Implementing Runnable interface
┌────────────────────┐
│ Runnable (interface)│
└────────┬───────────┘
         ↓ implements
┌────────────────────┐
│   MyRunnable       │
│   (implement run())│
└────────────────────┘
```

### 4.2 Method 1: Extending Thread Class

```java
class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(500);  // Sleep for 500ms
            } catch (InterruptedException e) {
                System.out.println("Thread interrupted");
            }
        }
    }
}

public class ThreadDemo1 {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.setName("Worker-Thread");
        t1.start();  // Calls run() in new thread
        
        // t1.run();  // WRONG! This runs in main thread (no new thread)
        
        System.out.println("Main thread continues...");
    }
}
```

### 4.3 Method 2: Implementing Runnable Interface (Preferred)

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                System.out.println("Thread interrupted");
            }
        }
    }
}

public class ThreadDemo2 {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread t1 = new Thread(myRunnable, "Runnable-Thread");
        t1.start();
        
        // Using Lambda (Java 8+)
        Thread t2 = new Thread(() -> {
            System.out.println("Lambda thread running");
        });
        t2.start();
    }
}
```

### 4.4 Thread vs Runnable Comparison

| Feature | extends Thread | implements Runnable |
|---------|---------------|---------------------|
| Inheritance | Cannot extend another class | Can extend another class |
| Reusability | Less reusable | More reusable |
| Object sharing | Each thread = separate object | Single object, multiple threads |
| Recommended | No | Yes (preferred) |

---

## 5. Creating Multiple Threads

```java
class NumberThread extends Thread {
    NumberThread(String name) {
        super(name);
    }
    
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(getName() + ": " + i);
            try { Thread.sleep(300); } catch (InterruptedException e) {}
        }
        System.out.println(getName() + " finished");
    }
}

public class MultiThreadDemo {
    public static void main(String[] args) {
        NumberThread t1 = new NumberThread("Thread-A");
        NumberThread t2 = new NumberThread("Thread-B");
        NumberThread t3 = new NumberThread("Thread-C");
        
        t1.start();
        t2.start();
        t3.start();
        
        System.out.println("Main thread finished");
    }
}
```

---

## 6. Using isAlive() and join()

### 6.1 isAlive()

Returns `true` if the thread is still running.

```java
Thread t1 = new Thread(() -> {
    try { Thread.sleep(2000); } catch(InterruptedException e) {}
});
t1.start();

System.out.println("Is alive? " + t1.isAlive());  // true
t1.join();  // Wait for t1 to finish
System.out.println("Is alive? " + t1.isAlive());  // false
```

### 6.2 join()

Causes the **calling thread to wait** until the specified thread finishes.

```java
public class JoinDemo {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread-1: " + i);
                try { Thread.sleep(500); } catch (InterruptedException e) {}
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread-2: " + i);
                try { Thread.sleep(500); } catch (InterruptedException e) {}
            }
        });
        
        t1.start();
        t1.join();   // Main waits for t1 to finish
        
        t2.start();
        t2.join();   // Main waits for t2 to finish
        
        System.out.println("Both threads completed!");
    }
}
// Result: t1 runs completely, then t2, then main continues
```

### 6.3 join(long milliseconds)

Waits for at most the specified time.

```java
t1.join(2000);  // Wait max 2 seconds for t1 to finish
```

---

## 7. wait(), notify(), and notifyAll()

### 7.1 Inter-Thread Communication

These methods are defined in the `Object` class and must be called from within a **synchronized** context.

| Method | Description |
|--------|-------------|
| `wait()` | Current thread releases lock and waits |
| `notify()` | Wakes up ONE waiting thread |
| `notifyAll()` | Wakes up ALL waiting threads |

### 7.2 Producer-Consumer Example (Exam Important ⭐)

```java
class SharedBuffer {
    private int data;
    private boolean hasData = false;
    
    // Producer puts data
    synchronized void produce(int value) {
        while (hasData) {
            try { wait(); }  // Wait until consumer consumes
            catch (InterruptedException e) {}
        }
        data = value;
        hasData = true;
        System.out.println("Produced: " + value);
        notify();  // Wake up consumer
    }
    
    // Consumer gets data
    synchronized int consume() {
        while (!hasData) {
            try { wait(); }  // Wait until producer produces
            catch (InterruptedException e) {}
        }
        hasData = false;
        System.out.println("Consumed: " + data);
        notify();  // Wake up producer
        return data;
    }
}

public class ProducerConsumer {
    public static void main(String[] args) {
        SharedBuffer buffer = new SharedBuffer();
        
        // Producer Thread
        Thread producer = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                buffer.produce(i);
            }
        });
        
        // Consumer Thread
        Thread consumer = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                buffer.consume();
            }
        });
        
        producer.start();
        consumer.start();
    }
}
/* Output:
   Produced: 1
   Consumed: 1
   Produced: 2
   Consumed: 2
   ...
*/
```

### 7.3 wait() vs sleep()

| Feature | wait() | sleep() |
|---------|--------|---------|
| **Class** | Object | Thread |
| **Lock** | Releases lock | Does NOT release lock |
| **Where** | Inside synchronized block | Anywhere |
| **Wake-up** | notify()/notifyAll() | Time expires |
| **Purpose** | Inter-thread communication | Pause execution |

---

## PART B: STRING HANDLING

---

## 8. String Class in Java

### 8.1 String is Immutable

Strings in Java are **immutable** — once created, their value cannot be changed.

```java
String s = "Hello";
s = s + " World";  // Creates a NEW String object
// Original "Hello" is still in memory (eligible for GC)
```

```
String Pool (Heap):
┌──────────────┐
│   "Hello"    │ ← Original (unchanged)
├──────────────┤
│"Hello World" │ ← New object created
└──────────────┘
      ↑
      s (reference now points here)
```

### 8.2 String Constructors

```java
// 1. String literal (String pool)
String s1 = "Hello";

// 2. Using new keyword (Heap)
String s2 = new String("Hello");

// 3. From char array
char[] chars = {'H', 'e', 'l', 'l', 'o'};
String s3 = new String(chars);

// 4. From char array subset
String s4 = new String(chars, 1, 3);  // "ell" (offset=1, count=3)

// 5. From byte array
byte[] bytes = {72, 101, 108, 108, 111};
String s5 = new String(bytes);  // "Hello"

// 6. From StringBuffer/StringBuilder
StringBuffer sb = new StringBuffer("Hello");
String s6 = new String(sb);
```

### 8.3 String Length

```java
String s = "Hello World";
int len = s.length();  // 11 (includes space)
System.out.println("Length: " + len);
```

---

## 9. Character Extraction

| Method | Description | Example |
|--------|-------------|---------|
| `charAt(int index)` | Returns char at index | `"Hello".charAt(1)` → `'e'` |
| `getChars(int, int, char[], int)` | Copies chars to array | See below |
| `toCharArray()` | Converts to char array | `"Hi".toCharArray()` → `{'H','i'}` |

```java
String s = "Hello World";

// charAt
char ch = s.charAt(0);   // 'H'

// getChars
char[] dest = new char[5];
s.getChars(0, 5, dest, 0);  // dest = {'H','e','l','l','o'}
// getChars(srcBegin, srcEnd, dest, destBegin)

// toCharArray
char[] arr = s.toCharArray();  // {'H','e','l','l','o',' ','W','o','r','l','d'}
```

---

## 10. String Comparison

| Method | Description | Example |
|--------|-------------|---------|
| `equals(String)` | Content equality (case-sensitive) | `"Hello".equals("Hello")` → `true` |
| `equalsIgnoreCase(String)` | Content equality (case-insensitive) | `"Hello".equalsIgnoreCase("hello")` → `true` |
| `compareTo(String)` | Lexicographic comparison | `"abc".compareTo("abd")` → `-1` |
| `==` | Reference comparison | Checks if same object in memory |
| `startsWith(String)` | Starts with prefix | `"Hello".startsWith("He")` → `true` |
| `endsWith(String)` | Ends with suffix | `"Hello".endsWith("lo")` → `true` |
| `contains(String)` | Contains substring | `"Hello".contains("ell")` → `true` |

```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");

// == vs equals
System.out.println(s1 == s2);       // true (same pool object)
System.out.println(s1 == s3);       // false (different objects)
System.out.println(s1.equals(s3));  // true (same content)

// compareTo
System.out.println("apple".compareTo("banana"));  // negative (a < b)
System.out.println("banana".compareTo("apple"));  // positive (b > a)
System.out.println("apple".compareTo("apple"));   // 0 (equal)
```

---

## 11. Modifying a String

Since Strings are **immutable**, modification methods return a **NEW String**.

| Method | Description | Example |
|--------|-------------|---------|
| `concat(String)` | Concatenate | `"Hello".concat(" World")` → `"Hello World"` |
| `substring(int)` | Substring from index | `"Hello".substring(2)` → `"llo"` |
| `substring(int, int)` | Substring range | `"Hello".substring(1,4)` → `"ell"` |
| `replace(char, char)` | Replace characters | `"Hello".replace('l','L')` → `"HeLLo"` |
| `toUpperCase()` | Convert to uppercase | `"Hello".toUpperCase()` → `"HELLO"` |
| `toLowerCase()` | Convert to lowercase | `"Hello".toLowerCase()` → `"hello"` |
| `trim()` | Remove leading/trailing spaces | `" Hi ".trim()` → `"Hi"` |
| `indexOf(String)` | Find first occurrence | `"Hello".indexOf("ll")` → `2` |
| `lastIndexOf(String)` | Find last occurrence | `"Hello".lastIndexOf("l")` → `3` |

```java
String s = "  Hello World  ";

System.out.println(s.trim());                   // "Hello World"
System.out.println(s.trim().toUpperCase());      // "HELLO WORLD"
System.out.println(s.trim().replace("World", "Java")); // "Hello Java"
System.out.println(s.trim().substring(6));       // "World"

// StringBuilder for mutable strings
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");     // "Hello World" (modifies same object)
sb.insert(5, ",");       // "Hello, World"
sb.delete(5, 6);         // "Hello World"
sb.reverse();            // "dlroW olleH"
```

### 11.1 String vs StringBuffer vs StringBuilder

| Feature | String | StringBuffer | StringBuilder |
|---------|--------|-------------|---------------|
| **Mutability** | Immutable | Mutable | Mutable |
| **Thread-safe** | Yes (immutable) | Yes (synchronized) | No |
| **Performance** | Slow (creates new objects) | Medium | Fast |
| **When to use** | Few modifications | Multi-threaded | Single-threaded |

---

## PART C: JAVA I/O

---

## 12. Java I/O Classes & Interfaces

### 12.1 I/O Stream Hierarchy

```
                     ┌─────────────────┐
                     │    java.io      │
                     └────────┬────────┘
              ┌───────────────┼───────────────┐
              ↓               ↓               ↓
       Byte Streams    Character Streams   Other
              │               │               │
       ┌──────┴──────┐ ┌─────┴──────┐    File
       ↓             ↓ ↓            ↓    Serializable
  InputStream   OutputStream Reader  Writer
```

### 12.2 Byte Streams (8-bit)

| Class | Description |
|-------|-------------|
| `InputStream` (abstract) | Base class for reading bytes |
| `OutputStream` (abstract) | Base class for writing bytes |
| `FileInputStream` | Read bytes from a file |
| `FileOutputStream` | Write bytes to a file |
| `BufferedInputStream` | Buffered reading for efficiency |
| `BufferedOutputStream` | Buffered writing for efficiency |
| `DataInputStream` | Read primitive data types |
| `DataOutputStream` | Write primitive data types |

```java
import java.io.*;

// Writing bytes to file
public class ByteStreamDemo {
    public static void main(String[] args) {
        // Writing
        try (FileOutputStream fos = new FileOutputStream("test.txt")) {
            String data = "Hello, Java I/O!";
            fos.write(data.getBytes());
            System.out.println("Data written successfully");
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Reading
        try (FileInputStream fis = new FileInputStream("test.txt")) {
            int ch;
            while ((ch = fis.read()) != -1) {
                System.out.print((char) ch);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 12.3 Character Streams (16-bit Unicode)

| Class | Description |
|-------|-------------|
| `Reader` (abstract) | Base class for reading characters |
| `Writer` (abstract) | Base class for writing characters |
| `FileReader` | Read characters from file |
| `FileWriter` | Write characters to file |
| `BufferedReader` | Buffered reading (readLine()) |
| `BufferedWriter` | Buffered writing |
| `PrintWriter` | Formatted output |

```java
import java.io.*;

public class CharStreamDemo {
    public static void main(String[] args) {
        // Writing using BufferedWriter
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
            bw.write("Line 1: Hello");
            bw.newLine();
            bw.write("Line 2: World");
            System.out.println("Written successfully");
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Reading using BufferedReader
        try (BufferedReader br = new BufferedReader(new FileReader("output.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 12.4 Byte Stream vs Character Stream

| Feature | Byte Stream | Character Stream |
|---------|------------|-----------------|
| Unit | 8-bit byte | 16-bit Unicode character |
| Classes | InputStream/OutputStream | Reader/Writer |
| Best for | Binary data (images, audio) | Text data |
| Encoding | No encoding | Supports encoding (UTF-8, etc.) |

---

## 13. Serialization

### 13.1 What is Serialization?

**Serialization** = Converting object state to a **byte stream** (to save to file or send over network)  
**Deserialization** = Converting byte stream back to an **object**

```
Object → Serialization → Byte Stream → File/Network
File/Network → Byte Stream → Deserialization → Object
```

### 13.2 Implementation

```java
import java.io.*;

// Class MUST implement Serializable
class Student implements Serializable {
    private static final long serialVersionUID = 1L;  // Version control
    
    String name;
    int rollNo;
    transient String password;  // transient = NOT serialized
    
    Student(String name, int rollNo, String password) {
        this.name = name;
        this.rollNo = rollNo;
        this.password = password;
    }
    
    @Override
    public String toString() {
        return "Student[name=" + name + ", rollNo=" + rollNo + 
               ", password=" + password + "]";
    }
}

public class SerializationDemo {
    public static void main(String[] args) {
        Student s = new Student("Rahul", 101, "secret123");
        
        // Serialization (Save object to file)
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream("student.ser"))) {
            oos.writeObject(s);
            System.out.println("Serialized: " + s);
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // Deserialization (Read object from file)
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream("student.ser"))) {
            Student loaded = (Student) ois.readObject();
            System.out.println("Deserialized: " + loaded);
            // Note: password will be null (transient)
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
/* Output:
   Serialized: Student[name=Rahul, rollNo=101, password=secret123]
   Deserialized: Student[name=Rahul, rollNo=101, password=null]
*/
```

### 13.3 Key Points

| Point | Description |
|-------|-------------|
| `Serializable` interface | Marker interface (no methods) |
| `transient` keyword | Field NOT serialized |
| `static` fields | NOT serialized (belong to class, not object) |
| `serialVersionUID` | Version control for compatibility |
| `ObjectOutputStream` | Used for serialization |
| `ObjectInputStream` | Used for deserialization |

---

## PART D: JDBC (Java Database Connectivity)

---

## 14. JDBC Fundamentals

### 14.1 What is JDBC?

**JDBC** is a Java API that allows Java programs to **connect to and interact with databases**.

### 14.2 JDBC Architecture

```
┌──────────────────┐
│  Java Application │
└────────┬─────────┘
         ↓
┌──────────────────┐
│   JDBC API       │  (java.sql package)
│ DriverManager    │
│ Connection       │
│ Statement        │
│ ResultSet        │
└────────┬─────────┘
         ↓
┌──────────────────┐
│  JDBC Driver     │  (Database specific)
└────────┬─────────┘
         ↓
┌──────────────────┐
│    Database      │  (MySQL, Oracle, PostgreSQL)
└──────────────────┘
```

### 14.3 Steps to Use JDBC

```java
import java.sql.*;

public class JDBCDemo {
    public static void main(String[] args) {
        try {
            // Step 1: Load the driver
            Class.forName("com.mysql.cj.jdbc.Driver");
            
            // Step 2: Establish connection
            Connection conn = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");
            
            // Step 3: Create statement
            Statement stmt = conn.createStatement();
            
            // Step 4: Execute query
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");
            
            // Step 5: Process results
            while (rs.next()) {
                System.out.println(rs.getInt("id") + " - " + 
                                 rs.getString("name") + " - " + 
                                 rs.getDouble("marks"));
            }
            
            // Step 6: Close connection
            rs.close();
            stmt.close();
            conn.close();
            
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 15. JDBC Driver Types (Exam Important ⭐)

### 15.1 Four Types of Drivers

```
Type 1: JDBC-ODBC Bridge
┌──────┐ → ┌──────┐ → ┌──────┐ → ┌────┐
│ Java │   │ JDBC │   │ ODBC │   │ DB │
│ App  │   │Bridge│   │Driver│   │    │
└──────┘   └──────┘   └──────┘   └────┘

Type 2: Native-API (Partially Java)
┌──────┐ → ┌──────┐ → ┌──────┐ → ┌────┐
│ Java │   │ JDBC │   │Native│   │ DB │
│ App  │   │Driver│   │ API  │   │    │
└──────┘   └──────┘   └──────┘   └────┘

Type 3: Network Protocol (Pure Java → Middleware)
┌──────┐ → ┌──────┐ → ┌──────────┐ → ┌────┐
│ Java │   │ JDBC │   │Middleware│   │ DB │
│ App  │   │Driver│   │ Server   │   │    │
└──────┘   └──────┘   └──────────┘   └────┘

Type 4: Thin Driver (Pure Java → Direct DB)
┌──────┐ → ┌──────┐ → ┌────┐
│ Java │   │ JDBC │   │ DB │
│ App  │   │Driver│   │    │
└──────┘   └──────┘   └────┘
```

### 15.2 Comparison Table

| Feature | Type 1 | Type 2 | Type 3 | Type 4 |
|---------|--------|--------|--------|--------|
| **Name** | JDBC-ODBC Bridge | Native API | Network Protocol | Thin Driver |
| **Platform** | Not portable | Not portable | Portable | Portable |
| **Performance** | Slow | Medium | Medium | Fast |
| **Pure Java?** | No | No (native) | Yes | Yes |
| **Client library** | ODBC required | DB client required | No | No |
| **Best for** | Testing only | Legacy systems | Web apps | Production |
| **Example** | sun.jdbc.odbc | Oracle OCI | IDS server | MySQL Connector/J |

> **For exams:** Type 4 (Thin Driver) is the **most commonly used** and **recommended** driver.

---

## PART E: NETWORKING

---

## 16. Networking Basics

### 16.1 Key Concepts

| Concept | Description |
|---------|-------------|
| **IP Address** | Unique identifier for a device on a network |
| **Port** | Logical endpoint for communication (0-65535) |
| **Protocol** | Rules for communication (TCP, UDP, HTTP) |
| **Socket** | Endpoint for two-way communication |
| **TCP** | Reliable, connection-oriented protocol |
| **UDP** | Fast, connectionless protocol |

### 16.2 Socket Overview

```
Client Machine                    Server Machine
┌─────────────┐                  ┌─────────────┐
│   Client    │                  │   Server    │
│   Socket    │ ←─── TCP ────→  │  ServerSocket│
│ (port auto) │   Connection    │  (port 8080) │
└─────────────┘                  └─────────────┘
```

### 16.3 Important Networking Classes

| Class | Description |
|-------|-------------|
| `InetAddress` | Represents an IP address |
| `Socket` | Client-side socket |
| `ServerSocket` | Server-side socket for accepting connections |
| `URL` | Represents a Uniform Resource Locator |
| `URLConnection` | Communicates with a URL resource |
| `DatagramSocket` | UDP socket |
| `DatagramPacket` | UDP packet |

---

## 17. TCP/IP Client Sockets

```java
import java.io.*;
import java.net.*;

// TCP Client
public class TCPClient {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 8080)) {
            
            // Send data to server
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            out.println("Hello Server!");
            
            // Receive data from server  
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream()));
            String response = in.readLine();
            System.out.println("Server says: " + response);
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 18. TCP/IP Server Sockets

```java
import java.io.*;
import java.net.*;

// TCP Server
public class TCPServer {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(8080)) {
            System.out.println("Server started on port 8080");
            
            while (true) {
                // Wait for client connection
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client connected: " + 
                    clientSocket.getInetAddress());
                
                // Read from client
                BufferedReader in = new BufferedReader(
                    new InputStreamReader(clientSocket.getInputStream()));
                String message = in.readLine();
                System.out.println("Client says: " + message);
                
                // Reply to client
                PrintWriter out = new PrintWriter(
                    clientSocket.getOutputStream(), true);
                out.println("Echo: " + message);
                
                clientSocket.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 19. URL and URLConnection

### 19.1 URL Format

```
protocol://hostname:port/path?query#fragment

Example:
https://www.example.com:443/api/users?page=1#results
  ↑          ↑           ↑     ↑        ↑      ↑
Protocol   Hostname    Port   Path    Query  Fragment
```

### 19.2 URL Class

```java
import java.net.*;

public class URLDemo {
    public static void main(String[] args) throws Exception {
        URL url = new URL("https://www.example.com:443/api/users?page=1");
        
        System.out.println("Protocol: " + url.getProtocol());   // https
        System.out.println("Host: " + url.getHost());            // www.example.com
        System.out.println("Port: " + url.getPort());            // 443
        System.out.println("Path: " + url.getPath());            // /api/users
        System.out.println("Query: " + url.getQuery());          // page=1
    }
}
```

### 19.3 URLConnection

```java
import java.io.*;
import java.net.*;

public class URLConnectionDemo {
    public static void main(String[] args) throws Exception {
        URL url = new URL("https://www.example.com");
        URLConnection conn = url.openConnection();
        
        // Read content
        BufferedReader br = new BufferedReader(
            new InputStreamReader(conn.getInputStream()));
        
        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
        br.close();
    }
}
```

### 19.4 Whois

```java
import java.io.*;
import java.net.*;

public class WhoisClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("whois.internic.net", 43);
        
        // Send domain query
        OutputStream out = socket.getOutputStream();
        String domain = "example.com\n";
        out.write(domain.getBytes());
        
        // Read response
        BufferedReader in = new BufferedReader(
            new InputStreamReader(socket.getInputStream()));
        String line;
        while ((line = in.readLine()) != null) {
            System.out.println(line);
        }
        
        socket.close();
    }
}
```

---

## 20. Important Exam Questions

### Short Answer Questions
1. What is a thread? Explain its life cycle with diagram.
2. Differentiate between `wait()` and `sleep()`.
3. What is synchronization? Why is it needed?
4. Differentiate between String, StringBuffer, and StringBuilder.
5. What is serialization? What is `transient` keyword?
6. List the four types of JDBC drivers. Which is most recommended?
7. What is a socket? Differentiate between TCP and UDP.

### Long Answer Questions
1. Explain the two ways to create a thread in Java with examples. Which is preferred and why?
2. Explain inter-thread communication using `wait()`, `notify()`, and `notifyAll()` with the Producer-Consumer example.
3. Explain JDBC with all four driver types and write a program to connect to a database.
4. Write a program demonstrating TCP/IP Client-Server communication in Java.
5. Explain String methods for comparison and modification with examples.
6. Explain serialization and deserialization with a complete example. What role does `transient` play?

---

> **Exam Tip:** For thread life cycle questions, always draw the **state transition diagram** showing all 6 states (New, Runnable, Blocked, Waiting, Timed Waiting, Terminated).
