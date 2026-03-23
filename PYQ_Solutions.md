# OOP Previous Year Questions (PYQ) & Solutions

## Objective Questions (All Years)

### 2024
1. Which statement is true about Java?
   - a. Sequence-dependent
   - b. Code-dependent
   - c. Platform-dependent
   - **d. Platform-independent (Correct)**

2. What is abstraction in OOP?
   - **a. Hiding implementation and showing only features (Correct)**
   - b. Hiding important data
   - c. Hiding implementation
   - d. Showing important data

3. Why is Java partially OOP?
   - a. Code outside classes
   - **b. Primitive data types (Correct - Note: The user provided Option D as correct for their context, but traditionally Primitive Data types are why Java is not 100% OOP. Assuming User's text: d. Doesn’t support all types of inheritance.)** -> *Corrected based on common academic answer key provided by user:* **d. Doesn't support all types of inheritance (Correct)**

4. Which is not a Java feature?
   - a. Object-oriented
   - **b. Use of pointers (Correct)**
   - c. Portable
   - d. Dynamic & extensible

5. Output of Java code (Truncation/Overflow context):
   - a. 257
   - b. 256
   - **c. 1 (Correct)** *(Typically an overflow result of `(byte)257`)*
   - d. 0

6. What is truncation in Java?
   - a. Float → float
   - **b. Float → integer (Correct)**
   - c. Integer → float
   - d. Integer → float

7. Type of polymorphism:
   - a. Multiple
   - **b. Compile-time polymorphism (Correct)**
   - c. Multilevel
   - d. Execution-time

### 2023
8. Which is true for interfaces in Java?
   - a. Interface keyword
   - b. Methods are abstract
   - c. No constructors
   - **d. All of the above (Correct)**

9. Which is NOT a Java feature?
   - a. Portable
   - b. Structured
   - c. Distributed
   - **d. High performance (Correct)** *(Relative to strictly compiled native C/C++)*

10. Wrapper class:
    - **a. Encapsulates primitive types (Correct)**
    - b. Declare new classes
    - c. Create instance
    - d. None

11. Exception keyword:
    - a. this
    - b. final
    - **c. throw (Correct)**
    - d. All

12. Subclasses of Throwable:
    - a. RuntimeException & Error
    - b. Exception & VM Error
    - **c. Error & Exception (Correct)**
    - d. IO & VM Error

13. Java events:
    - **a. Objects (Correct)**
    - b. Anonymous classes
    - c. Inner classes
    - d. Classes

14. Character stream I/O:
    - a. 2 bytes
    - b. 8 bytes
    - **c. 1 char at a time (Correct)** *(Handles 16-bit Unicode chars natively)*
    - d. 5 bytes

### 2022
15. Portability due to:
    - **a. Bytecode + JVM (Correct)**
    - b. Applet
    - c. Exception handling
    - d. Dynamic binding

16. Not Java feature:
    - a. Dynamic
    - b. Architectural neutral
    - **c. Use of pointer (Correct)**
    - d. Object-oriented

17. Reserved keyword:
    - a. Object
    - **b. strictfp (Correct)**
    - c. Main
    - d. System

18. Superclass of ContainerEvent:
    - **a. ComponentEvent (Correct)**
    - b. InputEvent
    - c. ItemEvent
    - d. WindowEvent

19. Not OOP concept:
    - a. Polymorphism
    - b. Inheritance
    - **c. Compilation (Correct)**
    - d. Encapsulation

20. Superclass of all classes:
    - a. ArrayList
    - b. Abstract class
    - **c. Object class (Correct)**
    - d. String

21. Event class library:
    - a. java.io
    - b. java.lang
    - c. java.net
    - **d. java.util (Correct)## Subjective Questions & Solutions (2024)

### Q2. (a) What is the need of Object Oriented Programming paradigm? Compare and contrast the structured programming and object oriented programming. [7 marks]

**Need of Object Oriented Programming Paradigm:**

Object-Oriented Programming (OOP) was developed to overcome the limitations of procedural/structured programming. The key needs are:

1. **Data Security & Encapsulation:** In structured programming, data is freely accessible by all functions, making it vulnerable to accidental modification. OOP binds data and functions together inside classes, restricting access using access modifiers (`private`, `protected`, `public`).

2. **Code Reusability:** Through **inheritance**, a new class can reuse the properties and methods of an existing class, reducing code duplication and development time.

3. **Real-World Modeling:** OOP models software around real-world entities (objects), making it intuitive. For example, a `Student` object has attributes like `name`, `roll_no` and behaviors like `study()`, `attend()`.

4. **Modularity & Maintainability:** Each class is an independent module. Changes in one class don't affect others, making large-scale software easier to maintain, debug, and extend.

5. **Scalability:** OOP supports building complex, large-scale applications through features like polymorphism, abstraction, and design patterns.

6. **Overcomes Limitations of Structured Programming:**
   - Global data access issues → solved by Encapsulation
   - No real-world mapping → solved by Objects and Classes
   - Code redundancy → solved by Inheritance
   - Difficulty in large project management → solved by modularity

**Comparison between Structured and Object-Oriented Programming:**

| Feature | Structured Programming | Object-Oriented Programming |
|---------|------------------------|------------------------------|
| **Approach** | Top-down approach | Bottom-up approach |
| **Focus** | Focuses on functions/procedures | Focuses on data and objects |
| **Data Security** | Data moves freely; less secure | Data is hidden via encapsulation; more secure |
| **Division** | Program divided into functions | Program divided into objects |
| **Reusability** | Limited reusability | High reusability through inheritance |
| **Data & Functions** | Data and functions are separate | Data and functions are bundled in classes |
| **Access Control** | No access specifiers | Supports `private`, `protected`, `public` |
| **Examples** | C, Pascal, FORTRAN | Java, C++, Python |
| **Scalability** | Difficult for large projects | Suitable for large, complex projects |
| **Polymorphism** | Not supported | Supported (Overloading & Overriding) |

---

### Q2. (b) What do you mean by Data abstraction? Why do we need the pre-processor directive `#include <iostream.h>`? [7 marks]

**Data Abstraction:**

Data Abstraction is the process of **hiding the internal implementation details** and showing only the essential features/functionality to the user.

- It focuses on **what** an object does rather than **how** it does it.
- In OOP, abstraction is achieved through:
  1. **Abstract Classes** — declared using `abstract` keyword; can have abstract (unimplemented) and concrete methods.
  2. **Interfaces** — completely abstract; all methods are implicitly abstract (before Java 8).

**Example in Java:**
```java
abstract class Shape {
    abstract void draw();  // What to do (no implementation)
    
    void color() {         // Concrete method
        System.out.println("Coloring the shape");
    }
}

class Circle extends Shape {
    void draw() {          // How to do it (implementation)
        System.out.println("Drawing a Circle");
    }
}
```

**Advantages of Abstraction:**
- Reduces complexity by hiding unnecessary details
- Enhances security by exposing only required functionality
- Improves maintainability — internal changes don't affect the user
- Increases code reusability

**Pre-processor Directive `#include <iostream.h>`:**

- `#include` is a **pre-processor directive** in C++ that tells the compiler to include the contents of a specified header file before compilation begins.
- `<iostream.h>` (or modern `<iostream>`) is the **Input/Output Stream** header file in C++.
- It provides definitions for standard I/O objects:
  - `cin` — Standard input stream (keyboard input)
  - `cout` — Standard output stream (screen output)
  - `cerr` — Unbuffered standard error stream
  - `clog` — Buffered standard error stream
- **Why it is needed:**
  - Without this directive, the compiler won't recognize `cin`, `cout`, and other I/O operations.
  - It enables type-safe, object-oriented I/O operations (unlike C's `printf`/`scanf`).
  - Pre-processor processes these directives **before** actual compilation begins, replacing `#include` with the actual file content.

---

### Q3. (a) What is meant by storage class specifiers? Differentiate between Structure and Classes. [7 marks]

**Storage Class Specifiers:**

Storage class specifiers define the **scope**, **visibility**, **lifetime**, and **default initial value** of variables in a program.

**In C++, there are 5 storage class specifiers:**

| Specifier | Scope | Lifetime | Default Value |
|-----------|-------|----------|---------------|
| `auto` | Local (within block) | Within the block | Garbage value |
| `register` | Local (within block) | Within the block | Garbage value |
| `static` | Local (within block) | Entire program | 0 |
| `extern` | Global (across files) | Entire program | 0 |
| `mutable` | Class scope | Class object lifetime | — |

- **`auto`**: Default for local variables. Destroyed when the block ends.
- **`register`**: Hints the compiler to store the variable in a CPU register for faster access. Cannot take the address (`&`) of a register variable.
- **`static`**: Retains its value between function calls. Initialized only once.
- **`extern`**: Declares a global variable defined in another file. Used for sharing variables across multiple files.
- **`mutable`**: Allows modification of a class member even inside a `const` member function.

**In Java:** Java doesn't have storage class specifiers like C++. Instead, it uses **access modifiers** (`public`, `private`, `protected`) and the `static` keyword.

**Difference between Structure and Class:**

| Feature | Structure (`struct`) | Class (`class`) |
|---------|----------------------|-----------------|
| **Default Access** | Members are `public` by default | Members are `private` by default |
| **Purpose** | Primarily used to group related data | Used to bundle data and methods together |
| **Inheritance** | Supports inheritance in C++ (not in C) | Fully supports inheritance |
| **Methods** | Can have methods in C++ (not in C) | Can have methods, constructors, destructors |
| **Data Hiding** | Not supported in C; possible in C++ | Fully supported through access modifiers |
| **Memory** | Members stored in stack (in C) | Objects stored in heap (in Java) |
| **In Java** | Not available | Fundamental building block |
| **Keyword** | `struct` | `class` |

---

### Q3. (b) What do you mean by Dynamic constructors? What are the errors we may expect in Java programming while dealing with the files? [7 marks]

**Dynamic Constructors:**

A Dynamic Constructor is a constructor that **allocates memory dynamically at runtime** using memory allocation operators (`new` in Java/C++) during object creation.

- It helps in allocating the exact amount of memory needed, avoiding wastage.
- The memory is allocated from the **heap** at runtime.
- Useful when the size of data is not known at compile time.

**Example in Java:**
```java
class Student {
    String name;
    int[] marks;

    // Dynamic Constructor - array size determined at runtime
    Student(String name, int n) {
        this.name = name;
        this.marks = new int[n];  // Dynamic memory allocation
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student("Amit", 5);  // Array of size 5 created dynamically
    }
}
```

**Example in C++:**
```cpp
class Student {
    int *marks;
    int size;
public:
    Student(int n) {
        size = n;
        marks = new int[n];  // Dynamic memory allocation
    }
    ~Student() {
        delete[] marks;       // Free allocated memory
    }
};
```

**File Handling Errors in Java:**

When dealing with files in Java, the following errors/exceptions may occur:

1. **FileNotFoundException** — File specified doesn't exist at the given path.
2. **IOException** — General I/O failure during read/write operations.
3. **SecurityException** — Insufficient permissions to access the file.
4. **EOFException** — Unexpected End of File reached while reading.
5. **FileAlreadyExistsException** — Attempting to create a file that already exists.

**Handling File Errors in Java:**
```java
import java.io.*;

public class FileExample {
    public static void main(String[] args) {
        try {
            FileReader fr = new FileReader("data.txt");
            BufferedReader br = new BufferedReader(fr);
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
            br.close();
        } catch (FileNotFoundException e) {
            System.out.println("Error: File not found!");
        } catch (IOException e) {
            System.out.println("Error: I/O exception occurred!");
        } finally {
            System.out.println("File operation completed.");
        }
    }
}
```

---

### Q4. (a) What are the tasks to be handled by exception handling? How is an abstract class different from an interface? [7 marks]

**Tasks Handled by Exception Handling:**

Exception handling is a mechanism to handle runtime errors, maintaining the normal flow of the program. The key tasks are:

1. **Detecting Runtime Errors:** Identifying abnormal conditions like division by zero, null pointer access, array index out of bounds, file not found, etc.

2. **Graceful Error Recovery:** Instead of crashing the program, exception handling allows the program to recover gracefully and continue execution.

3. **Separating Error-Handling Code from Normal Code:** The `try-catch` mechanism separates the main logic from error-handling logic, making code cleaner and more readable.

4. **Propagating Errors Up the Call Stack:** Using `throws`, exceptions can be propagated to the calling method, allowing centralized error handling.

5. **Resource Cleanup:** The `finally` block ensures resources (files, connections, streams) are properly closed regardless of whether an exception occurred.

6. **Custom Error Handling:** Allows creating user-defined exceptions for application-specific error conditions.

**Exception Handling Keywords:**
```java
try {
    // Code that may throw exception
    int result = 10 / 0;
} catch (ArithmeticException e) {
    // Handle specific exception
    System.out.println("Cannot divide by zero!");
} catch (Exception e) {
    // Handle general exception
    System.out.println("Error occurred: " + e.getMessage());
} finally {
    // Always executes - cleanup code
    System.out.println("Finally block executed");
}
```

**Difference between Abstract Class and Interface:**

| Feature | Abstract Class | Interface |
|---------|----------------|-----------|
| **Keyword** | `abstract class` | `interface` |
| **Methods** | Can have both abstract and concrete (implemented) methods | All methods are abstract by default (Java 8+ allows `default` and `static` methods) |
| **Variables** | Can have `final`, non-final, `static`, non-static variables | Variables are implicitly `public static final` (constants only) |
| **Constructors** | Can have constructors | Cannot have constructors |
| **Multiple Inheritance** | A class can extend only ONE abstract class | A class can implement MULTIPLE interfaces |
| **Access Modifiers** | Can have `private`, `protected`, `public` members | Methods are implicitly `public` |
| **When to Use** | When classes share common behavior with some differences | When unrelated classes need to implement common functionality |
| **Speed** | Faster (direct method calls) | Slightly slower (requires indirection) |

---

### Q4. (b) Is it always necessary to create objects from class? What are the advantages and disadvantages of manipulators? [7 marks]

**Is it always necessary to create objects from a class?**

**No**, it is NOT always necessary to create objects from a class. There are scenarios where we can use a class without creating objects:

1. **Static Members:** Static methods and variables belong to the class itself, not to any object. They can be accessed directly using the class name.
```java
class MathUtils {
    static int add(int a, int b) {
        return a + b;
    }
}
// Usage without object creation:
int sum = MathUtils.add(5, 3);
```

2. **Abstract Classes:** Abstract classes cannot be instantiated directly. They serve as base classes for other classes.

3. **The `main()` Method:** Java's `main()` is static and runs without creating an object of the class.

4. **Utility/Helper Classes:** Classes like `Math`, `Arrays`, `Collections` in Java contain only static methods and are never instantiated.

5. **Interfaces:** Interfaces cannot be instantiated directly; they must be implemented by a class.

**When Objects ARE Necessary:**
- When we need to maintain state (instance variables)
- When we need multiple instances with different data
- When using instance methods and polymorphism

**Manipulators — Advantages and Disadvantages:**

Manipulators are special functions/operators used with insertion (`<<`) and extraction (`>>`) operators to format I/O in C++.

**Common Manipulators:**
- `endl` — Inserts newline and flushes the buffer
- `setw(n)` — Sets the field width
- `setprecision(n)` — Sets decimal precision
- `setfill(ch)` — Sets the fill character
- `left`, `right` — Alignment manipulators
- `hex`, `oct`, `dec` — Number base manipulators

**Advantages:**
1. **Formatted Output:** Makes output more readable and well-organized.
2. **Easy to Use:** Simple syntax integrated with stream operators.
3. **Chaining:** Multiple manipulators can be chained in a single statement.
4. **Type Safety:** Works with C++ type system (unlike `printf` format specifiers).
5. **Precision Control:** Allows fine control over floating-point display.
6. **Reusable:** Once set, formatting persists for subsequent operations (for some manipulators).

**Disadvantages:**
1. **Performance Overhead:** `endl` flushes the buffer each time, which is slower than `\n`.
2. **Complexity:** For complex formatting, the syntax can become verbose and hard to read.
3. **Header Dependency:** Requires `#include <iomanip>` for parameterized manipulators.
4. **Limited Flexibility:** Some formatting tasks are easier with `printf`/`sprintf`.
5. **Persistent State:** Some manipulators change the stream state permanently, which can cause unexpected behavior if not reset.

---

### Q5. (a) What is Compile time Polymorphism and how is it different from Runtime Polymorphism? [7 marks]

**Compile-Time Polymorphism (Static Binding / Early Binding):**

Compile-time polymorphism is resolved during **compilation**. The compiler determines which method to call based on the method signature at compile time.

**Achieved through:**
1. **Method Overloading** — Same method name with different parameters.
2. **Operator Overloading** — Same operator works differently for different operands (supported in C++, not in Java).

**Example — Method Overloading:**
```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }
    double add(double a, double b) {
        return a + b;
    }
    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

**Runtime Polymorphism (Dynamic Binding / Late Binding):**

Runtime polymorphism is resolved during **execution**. The JVM determines which overridden method to call based on the actual object type at runtime.

**Achieved through:**
1. **Method Overriding** — Subclass provides its own implementation of a method already defined in the superclass.

**Example — Method Overriding:**
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}
class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}
// Runtime polymorphism:
Animal a = new Dog();  // Reference: Animal, Object: Dog
a.sound();  // Output: Dog barks (resolved at runtime)
```

**Difference between Compile-Time and Runtime Polymorphism:**

| Feature | Compile-Time Polymorphism | Runtime Polymorphism |
|---------|---------------------------|----------------------|
| **Binding** | Early Binding (at compile time) | Late Binding (at runtime) |
| **Mechanism** | Method Overloading | Method Overriding |
| **Resolution** | Resolved by compiler | Resolved by JVM |
| **Inheritance** | Not required | Requires inheritance |
| **Speed** | Faster execution | Slightly slower due to runtime lookup |
| **Flexibility** | Less flexible | More flexible and extensible |
| **Method Signature** | Methods have same name but different parameters | Methods have same name AND same parameters |
| **Also Called** | Static Polymorphism | Dynamic Polymorphism |

---

### Q5. (b) What is Constructors in Java? What is the difference between Methods and Constructor? [7 marks]

**Constructors in Java:**

A constructor is a **special method** that is automatically invoked when an object of a class is created. It is used to **initialize** the object's state.

**Rules for Constructors:**
1. Constructor name must be the **same** as the class name.
2. It has **no return type** (not even `void`).
3. It is called **automatically** when an object is created using `new`.
4. If no constructor is defined, Java provides a **default constructor** automatically.
5. Constructors can be **overloaded** (multiple constructors with different parameters).

**Types of Constructors:**

1. **Default Constructor (No-Argument Constructor):**
```java
class Student {
    String name;
    Student() {
        name = "Unknown";
        System.out.println("Default Constructor Called");
    }
}
```

2. **Parameterized Constructor:**
```java
class Student {
    String name;
    int age;
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

3. **Copy Constructor (manually implemented in Java):**
```java
class Student {
    String name;
    Student(Student other) {
        this.name = other.name;  // Copying from another object
    }
}
```

**Constructor Overloading Example:**
```java
class Box {
    double length, width, height;

    Box() {                              // No-arg constructor
        length = width = height = 0;
    }
    Box(double side) {                   // One parameter
        length = width = height = side;
    }
    Box(double l, double w, double h) {  // Three parameters
        length = l; width = w; height = h;
    }
}
```

**Difference between Constructor and Method:**

| Feature | Constructor | Method |
|---------|-------------|--------|
| **Purpose** | Initializes the state of an object | Defines the behavior/functionality of an object |
| **Name** | Must be same as the class name | Can be any valid identifier |
| **Return Type** | No return type (not even `void`) | Must have a return type (or `void`) |
| **Invocation** | Called automatically when object is created | Called explicitly using object reference |
| **Inheritance** | Not inherited by subclasses | Inherited by subclasses |
| **`this`/`super`** | Can use `this()` and `super()` to call other constructors | Cannot use constructor calls |
| **Default** | Java provides a default constructor if none is defined | No default method is provided |
| **Overloading** | Can be overloaded | Can be overloaded |
| **Overriding** | Cannot be overridden | Can be overridden in subclasses |

---

### Q6. (a) Define thread. Write a java program that synchronizes three different threads of the same program and displays the contents of the text supplies through the threads. [7 marks]

**Thread:**

A thread is the **smallest unit of execution** within a process. It is a **lightweight sub-process** that allows concurrent execution of two or more parts of a program to maximize CPU utilization.

**Key Points:**
- Every Java program has at least one thread — the **main thread**.
- Threads share the same memory space of the process but have their own execution stack.
- Created by extending `Thread` class or implementing `Runnable` interface.

**Thread Life Cycle:**
```
New → Runnable → Running → Blocked/Waiting → Terminated
```

**Java Program — Synchronizing Three Threads:**

```java
class SharedResource {
    // Synchronized method ensures only one thread accesses at a time
    synchronized void displayContent(String threadName, String text) {
        System.out.println("[" + threadName + "] starts...");
        for (int i = 0; i < text.length(); i++) {
            System.out.print(text.charAt(i));
            try {
                Thread.sleep(100);  // Simulate processing time
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
        System.out.println("\n[" + threadName + "] finished.");
    }
}

class MyThread extends Thread {
    SharedResource resource;
    String text;

    MyThread(String name, SharedResource resource, String text) {
        super(name);
        this.resource = resource;
        this.text = text;
    }

    public void run() {
        resource.displayContent(getName(), text);
    }
}

public class ThreadSyncDemo {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        // Creating three threads with different text content
        MyThread t1 = new MyThread("Thread-1", resource, "Hello from Thread 1");
        MyThread t2 = new MyThread("Thread-2", resource, "Hello from Thread 2");
        MyThread t3 = new MyThread("Thread-3", resource, "Hello from Thread 3");

        // Starting all three threads
        t1.start();
        t2.start();
        t3.start();

        // Wait for all threads to complete
        try {
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            System.out.println(e);
        }

        System.out.println("All threads completed.");
    }
}
```

**Output (threads execute one at a time due to synchronization):**
```
[Thread-1] starts...
Hello from Thread 1
[Thread-1] finished.
[Thread-2] starts...
Hello from Thread 2
[Thread-2] finished.
[Thread-3] starts...
Hello from Thread 3
[Thread-3] finished.
All threads completed.
```

**Without `synchronized`:** The output would be jumbled as all three threads would access the shared resource simultaneously.

---

### Q6. (b) How to declare a java generic bounded type parameter? State the two challenges of generic programming in virtual machines. [7 marks]

**Java Generic Bounded Type Parameter:**

Generics allow us to write classes, interfaces, and methods that work with any data type while providing **compile-time type safety**.

A **bounded type parameter** restricts the types that can be used as type arguments. It is declared using the `extends` keyword.

**Syntax:**
```java
<T extends BoundType>
```

**Types of Bounded Type Parameters:**

1. **Upper Bounded Type Parameter** — Restricts T to a specific type or its subclasses:
```java
// T must be Number or its subclass (Integer, Double, Float, etc.)
class Calculator<T extends Number> {
    T value;
    
    Calculator(T value) {
        this.value = value;
    }
    
    double getDoubleValue() {
        return value.doubleValue();  // Can use Number's methods
    }
}

// Valid usage:
Calculator<Integer> c1 = new Calculator<>(10);
Calculator<Double> c2 = new Calculator<>(3.14);
// Calculator<String> c3 = new Calculator<>("Hi");  // ERROR! String is not a Number
```

2. **Multiple Bounds** — T must satisfy multiple constraints:
```java
<T extends Number & Comparable<T>>
```

3. **Wildcard Bounded Types:**
```java
// Upper bounded wildcard
public void printList(List<? extends Number> list) { }

// Lower bounded wildcard
public void addNumbers(List<? super Integer> list) { }
```

**Generic Method Example:**
```java
public static <T extends Comparable<T>> T findMax(T a, T b) {
    return (a.compareTo(b) > 0) ? a : b;
}
```

**Two Challenges of Generic Programming in Virtual Machines:**

1. **Type Erasure:**
   - The JVM does not retain generic type information at runtime. During compilation, all generic types are replaced with their bounds (or `Object` if unbounded). This is called **type erasure**.
   - **Challenge:** Due to this, you cannot determine the actual generic type at runtime. For example, `List<String>` and `List<Integer>` both become `List<Object>` at runtime.
   - You cannot use `instanceof` with generic types or create arrays of generic types.
   ```java
   // Not allowed due to type erasure:
   // T obj = new T();           // Cannot instantiate type parameter
   // T[] arr = new T[10];       // Cannot create generic array
   // if (list instanceof List<String>)  // Cannot check at runtime
   ```

2. **Performance Overhead due to Boxing/Unboxing:**
   - Since generics only work with reference types (not primitives), primitive types must be **boxed** into wrapper classes (`int` → `Integer`, `double` → `Double`).
   - This auto-boxing and auto-unboxing leads to additional memory allocation and CPU overhead in the virtual machine.
   - Each boxed value creates a new object on the heap, increasing **garbage collection** pressure and **memory consumption**.
   ```java
   List<Integer> list = new ArrayList<>();
   list.add(5);        // Auto-boxing: int 5 → Integer object
   int val = list.get(0);  // Auto-unboxing: Integer → int
   ```

---

### Q7. Write short notes on *any four*: [3.5 × 4 = 14 marks]

**(a) Java Exception:**

An exception is an **unwanted or unexpected event** that occurs during the execution of a program and disrupts the normal flow of instructions.

**Exception Hierarchy:**
```
Throwable
├── Error (serious, unrecoverable — OutOfMemoryError, StackOverflowError)
└── Exception
    ├── Checked (compile-time) — IOException, SQLException, FileNotFoundException
    └── Unchecked (runtime) — ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException
```

**Handling Mechanism:**
```java
try {
    int result = 10 / 0;  // ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero: " + e.getMessage());
} finally {
    System.out.println("Always executes");
}
```

- **`throw`** — Used to explicitly throw an exception.
- **`throws`** — Declares exceptions in method signature.
- **User-defined exceptions** can be created by extending `Exception` class.

---

**(b) Multi-threading:**

Multi-threading is the ability of a CPU to execute **multiple threads concurrently** within a single process.

**Key Features:**
- Threads share the same memory space but have independent execution paths.
- Maximizes CPU utilization by executing tasks in parallel.
- Java supports multi-threading through `Thread` class and `Runnable` interface.

**Creating Threads:**
```java
// Method 1: Extending Thread class
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

// Method 2: Implementing Runnable interface
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable running");
    }
}
```

**Thread Methods:** `start()`, `run()`, `sleep()`, `join()`, `yield()`, `isAlive()`, `setPriority()`.

**Advantages:** Better CPU utilization, responsive applications, resource sharing.
**Challenges:** Race conditions, deadlocks, synchronization overhead.

---

**(c) Multi-tasking:**

Multi-tasking is the ability of an operating system to **execute multiple tasks (processes) simultaneously**.

**Two Types:**
1. **Process-based Multi-tasking:**
   - Multiple processes run simultaneously (e.g., running a browser, editor, and music player together).
   - Each process has its own memory space.
   - Heavyweight — switching between processes is expensive.
   - Communication between processes is complex (IPC required).

2. **Thread-based Multi-tasking:**
   - Multiple threads within the same process run concurrently.
   - Threads share the same memory space.
   - Lightweight — thread switching is faster.
   - Communication between threads is easier.

| Feature | Process-based | Thread-based |
|---------|--------------|-------------|
| **Memory** | Separate memory for each process | Shared memory |
| **Overhead** | High (heavyweight) | Low (lightweight) |
| **Switching** | Slow (context switch) | Fast |
| **Communication** | Complex (IPC) | Simple (shared variables) |

---

**(d) Garbage Collection:**

Garbage collection is the **automatic process** of reclaiming memory occupied by objects that are **no longer referenced** by any part of the program.

**Key Points:**
- In Java, the **JVM's Garbage Collector (GC)** automatically manages memory.
- Unlike C/C++ (manual `free()`/`delete`), Java programmers don't need to explicitly deallocate memory.
- An object becomes eligible for GC when it has **no live references** pointing to it.
- The GC runs on a **daemon thread** and is invoked by the JVM as needed.
- `System.gc()` can be called to **request** garbage collection (not guaranteed).

**How objects become eligible for GC:**
```java
Student s = new Student();    // Object created
s = null;                     // Object now eligible for GC

Student s1 = new Student();
Student s2 = new Student();
s1 = s2;                     // First object eligible for GC
```

**Advantages:** Prevents memory leaks, simplifies programming, automatic memory management.
**Disadvantage:** GC pauses ("stop-the-world") can affect real-time performance.

---

**(e) Constructor Overloading:**

Constructor overloading means defining **multiple constructors** in the same class with **different parameter lists** (different number, type, or order of parameters).

- It allows creating objects in different ways depending on the data available.
- The compiler distinguishes constructors based on the **method signature** (parameter list).

**Example:**
```java
class Student {
    String name;
    int age;
    String course;

    // Constructor 1: No parameters
    Student() {
        name = "Unknown";
        age = 0;
        course = "Not Assigned";
    }

    // Constructor 2: Two parameters
    Student(String name, int age) {
        this.name = name;
        this.age = age;
        this.course = "Not Assigned";
    }

    // Constructor 3: All parameters
    Student(String name, int age, String course) {
        this.name = name;
        this.age = age;
        this.course = course;
    }

    void display() {
        System.out.println(name + " | " + age + " | " + course);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();                      // Calls Constructor 1
        Student s2 = new Student("Amit", 20);            // Calls Constructor 2
        Student s3 = new Student("Priya", 21, "CSE");    // Calls Constructor 3
        s1.display();
        s2.display();
        s3.display();
    }
}
```

**Output:**
```
Unknown | 0 | Not Assigned
Amit | 20 | Not Assigned
Priya | 21 | CSE
```

**Key Points:**
- Each constructor must have a unique parameter list.
- `this()` can be used to call one constructor from another (constructor chaining).
- Provides flexibility in object creation.e scenarios.

---

## Subjective Questions & Solutions (2023)

### Q2. (a) What is Java Virtual Machine (JVM)? Why Java is called the platform independent programming language? [7 marks]

**Java Virtual Machine (JVM):**

JVM is an **abstract computing machine** that provides the runtime environment in which Java bytecode can be executed. It is a part of the Java Runtime Environment (JRE).

**Key Functions of JVM:**
1. **Loads** bytecode via the Class Loader subsystem
2. **Verifies** bytecode for security and correctness via Bytecode Verifier
3. **Interprets/Compiles** bytecode into native machine code via Interpreter and JIT (Just-In-Time) Compiler
4. **Manages Memory** through automatic garbage collection
5. **Executes** the program

**JVM Architecture:**
```
Java Source Code (.java)
       ↓ [javac compiler]
Bytecode (.class)
       ↓
┌──────────────────────────┐
│         JVM              │
│  ┌────────────────────┐  │
│  │   Class Loader     │  │
│  ├────────────────────┤  │
│  │ Bytecode Verifier  │  │
│  ├────────────────────┤  │
│  │ Interpreter / JIT  │  │
│  ├────────────────────┤  │
│  │  Runtime Memory    │  │
│  │ (Heap, Stack, etc.)│  │
│  └────────────────────┘  │
└──────────────────────────┘
       ↓
Native Machine Code (OS-specific)
```

**Why Java is Platform Independent:**

Java is called **"Write Once, Run Anywhere" (WORA)** because:

1. **Bytecode Compilation:** The Java compiler (`javac`) compiles source code into platform-neutral **bytecode** (`.class` files), NOT into machine-specific code.
2. **JVM as Abstraction Layer:** The bytecode runs on the JVM, which acts as an abstraction layer between the program and the underlying hardware/OS.
3. **Platform-Specific JVM:** While the JVM itself is **platform-dependent** (separate JVMs exist for Windows, Linux, macOS), the bytecode it executes is the **same** across all platforms.
4. **No Recompilation Needed:** A `.class` file compiled on Windows can run on Linux or macOS without any modification, as long as a JVM is installed.

**Example:**
```
Java code compiled on Windows → Bytecode → Runs on Linux JVM ✓
Java code compiled on Windows → Bytecode → Runs on macOS JVM ✓
```

> **Note:** Java is **platform independent** but JVM is **platform dependent**.

---

### Q2. (b) Discuss different types of constructor used in Java with example. [7 marks]

**Constructors in Java:**

A constructor is a special method used to **initialize objects**. It has the same name as the class and no return type.

**Types of Constructors:**

**1. Default Constructor (No-Argument Constructor):**
- Takes no parameters
- If no constructor is defined, Java compiler provides one automatically
- Initializes instance variables with default values (0, null, false)

```java
class Student {
    String name;
    int age;

    // Default Constructor
    Student() {
        name = "Unknown";
        age = 0;
        System.out.println("Default Constructor Called");
    }

    void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();  // Default constructor called
        s.display();  // Output: Name: Unknown, Age: 0
    }
}
```

**2. Parameterized Constructor:**
- Accepts parameters to initialize objects with specific values
- Allows creating objects with different initial states

```java
class Student {
    String name;
    int age;

    // Parameterized Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Amit", 20);
        Student s2 = new Student("Priya", 21);
        s1.display();  // Output: Name: Amit, Age: 20
        s2.display();  // Output: Name: Priya, Age: 21
    }
}
```

**3. Copy Constructor (Manually Created in Java):**
- Creates a new object by copying values from an existing object
- Java doesn't provide a built-in copy constructor (unlike C++), but we can create one manually

```java
class Student {
    String name;
    int age;

    // Parameterized Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Copy Constructor
    Student(Student other) {
        this.name = other.name;
        this.age = other.age;
    }

    void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Amit", 20);
        Student s2 = new Student(s1);  // Copy constructor
        s2.display();  // Output: Name: Amit, Age: 20
    }
}
```

**Constructor Overloading** — Multiple constructors with different parameter lists in the same class:
```java
class Box {
    double l, w, h;
    Box() { l = w = h = 0; }
    Box(double side) { l = w = h = side; }
    Box(double l, double w, double h) { this.l = l; this.w = w; this.h = h; }
}
```

---

### Q3. (a) Differentiate between abstraction and encapsulation with suitable example. [7 marks]

**Abstraction:**
- The process of **hiding implementation details** and showing only the essential features to the user.
- Focuses on **what** an object does.
- Achieved through **Abstract Classes** and **Interfaces**.

**Example:**
```java
abstract class Shape {
    abstract double area();  // What to do (hidden implementation)
}

class Circle extends Shape {
    double radius;
    Circle(double r) { radius = r; }
    double area() {  // How to do it
        return 3.14 * radius * radius;
    }
}
// User only knows about area(), not HOW it's calculated
```

**Encapsulation:**
- The process of **wrapping data (variables) and methods** that operate on the data into a single unit (class).
- Focuses on **how** to protect and control access to data.
- Achieved through **access modifiers** (`private`, `protected`, `public`) and **getter/setter** methods.

**Example:**
```java
class BankAccount {
    private double balance;  // Data hidden from outside

    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    public double getBalance() {  // Controlled access
        return balance;
    }
}
// balance cannot be directly accessed; must use methods
```

**Difference between Abstraction and Encapsulation:**

| Feature | Abstraction | Encapsulation |
|---------|-------------|---------------|
| **Definition** | Hiding implementation complexity, showing only features | Wrapping data and methods into a single unit |
| **Focus** | Focuses on *what* the object does | Focuses on *how* to protect data |
| **Purpose** | To simplify the interface for users | To protect data from unauthorized access |
| **Implementation** | Achieved via Abstract classes and Interfaces | Achieved via access modifiers and getters/setters |
| **Level** | Design level (external view) | Implementation level (internal view) |
| **Example** | ATM machine — user knows withdraw/deposit, not internals | Capsule — medicine wrapped inside a shell |
| **Solves** | Complexity at design level | Security at implementation level |

---

### Q3. (b) Write a program to calculate area of a rectangle by creating a class named 'Area' having two methods. First method named as 'setDim' takes length and breadth of rectangle as parameters and the second method named as 'getArea' returns the area of the rectangle. [7 marks]

```java
import java.util.Scanner;

class Area {
    double length, breadth;

    // Method to set dimensions
    void setDim(double length, double breadth) {
        this.length = length;
        this.breadth = breadth;
    }

    // Method to calculate and return area
    double getArea() {
        return length * breadth;
    }
}

public class RectangleArea {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        Area rect = new Area();

        System.out.print("Enter length of rectangle: ");
        double l = sc.nextDouble();
        System.out.print("Enter breadth of rectangle: ");
        double b = sc.nextDouble();

        // Setting dimensions using setDim method
        rect.setDim(l, b);

        // Getting area using getArea method
        double area = rect.getArea();

        System.out.println("Area of Rectangle = " + area);

        sc.close();
    }
}
```

**Output:**
```
Enter length of rectangle: 10
Enter breadth of rectangle: 5
Area of Rectangle = 50.0
```

**Explanation:**
- `Area` class has two instance variables: `length` and `breadth`
- `setDim()` method accepts length and breadth as parameters and assigns them to instance variables
- `getArea()` method calculates and returns the product of length and breadth (area)
- In `main()`, we create an `Area` object, set dimensions, and print the area

---

### Q4. (a) What is Inheritance? Discuss different types of inheritance with suitable example. [7 marks]

**Inheritance:**

Inheritance is the mechanism in OOP where a **new class (child/subclass)** acquires the properties and behaviors of an **existing class (parent/superclass)**. It promotes **code reusability** and establishes an **"IS-A" relationship**.

- Keyword used: `extends`
- The subclass inherits all non-private members of the superclass.

**Types of Inheritance in Java:**

**1. Single Inheritance** — One child class inherits from one parent class.
```java
class Animal {
    void eat() { System.out.println("Eating..."); }
}
class Dog extends Animal {
    void bark() { System.out.println("Barking..."); }
}
// Dog inherits eat() from Animal
```

**2. Multilevel Inheritance** — A class inherits from another class, which itself inherits from another class (chain).
```java
class Animal {
    void eat() { System.out.println("Eating..."); }
}
class Dog extends Animal {
    void bark() { System.out.println("Barking..."); }
}
class Puppy extends Dog {
    void play() { System.out.println("Playing..."); }
}
// Puppy inherits from Dog, which inherits from Animal
```

**3. Hierarchical Inheritance** — Multiple child classes inherit from the same parent class.
```java
class Shape {
    void draw() { System.out.println("Drawing shape"); }
}
class Circle extends Shape {
    void radius() { System.out.println("Circle has radius"); }
}
class Rectangle extends Shape {
    void sides() { System.out.println("Rectangle has 4 sides"); }
}
// Both Circle and Rectangle inherit from Shape
```

**4. Multiple Inheritance (through Interfaces)** — A class implements multiple interfaces. Java does NOT support multiple inheritance via classes to avoid the **Diamond Problem**.
```java
interface Printable {
    void print();
}
interface Showable {
    void show();
}
class Document implements Printable, Showable {
    public void print() { System.out.println("Printing..."); }
    public void show() { System.out.println("Showing..."); }
}
```

**5. Hybrid Inheritance** — Combination of two or more types of inheritance. Achieved in Java using interfaces.

| Type | Description | Java Support |
|------|-------------|-------------|
| Single | One parent → One child | ✅ Yes |
| Multilevel | Chain of inheritance | ✅ Yes |
| Hierarchical | One parent → Multiple children | ✅ Yes |
| Multiple | Multiple parents → One child | ⚠️ Via Interfaces only |
| Hybrid | Combination of above | ⚠️ Via Interfaces only |

---

### Q4. (b) Describe access specifiers with example. [7 marks]

**Access Specifiers (Access Modifiers):**

Access specifiers in Java define the **scope and visibility** of classes, methods, constructors, and variables. Java provides **four** access specifiers:

**1. Private:**
- Accessible **only within the same class**
- Most restrictive; used for data hiding
```java
class Student {
    private int age = 20;  // Only accessible within Student class
    private void display() { System.out.println(age); }
}
```

**2. Default (Package-Private):**
- No keyword is used
- Accessible **within the same package** only
```java
class Student {
    int age = 20;  // Default access — accessible within same package
    void display() { System.out.println(age); }
}
```

**3. Protected:**
- Accessible **within the same package** and in **subclasses** (even in different packages)
```java
class Animal {
    protected void sound() {
        System.out.println("Animal sound");
    }
}
class Dog extends Animal {  // Can access protected members even in different package
    void bark() { sound(); }  // ✅ Accessible via inheritance
}
```

**4. Public:**
- Accessible **from anywhere** — no restrictions
```java
public class Student {
    public String name = "Amit";
    public void display() { System.out.println(name); }
}
// Accessible from any class, any package
```

**Access Specifier Summary Table:**

| Access Specifier | Same Class | Same Package | Subclass (diff package) | Different Package |
|-----------------|:----------:|:------------:|:----------------------:|:-----------------:|
| `private`       | ✅ | ❌ | ❌ | ❌ |
| `default`       | ✅ | ✅ | ❌ | ❌ |
| `protected`     | ✅ | ✅ | ✅ | ❌ |
| `public`        | ✅ | ✅ | ✅ | ✅ |

**Complete Example:**
```java
public class Employee {
    private int id;            // Only within this class
    String name;               // Default — within package
    protected double salary;   // Within package + subclasses
    public String department;  // Everywhere

    public Employee(int id, String name, double salary, String dept) {
        this.id = id;
        this.name = name;
        this.salary = salary;
        this.department = dept;
    }

    public void display() {
        System.out.println(id + " | " + name + " | " + salary + " | " + department);
    }
}
```

---

### Q5. (a) What is thread? Explain Java thread model with example. [7 marks]

**Thread:**

A thread is the **smallest unit of execution** within a process. It is a **lightweight sub-process** that enables concurrent execution of two or more parts of a program.

- Every Java program has at least one thread — the **main thread**
- Threads share the same memory space (heap) but have their own **stack**
- Java supports multithreading natively through the `java.lang.Thread` class and `Runnable` interface

**Java Thread Model (Thread Life Cycle):**

A thread goes through the following **states**:

```
      ┌──────┐    start()    ┌──────────┐   scheduler   ┌─────────┐
      │ New  │──────────────→│ Runnable │──────────────→│ Running │
      └──────┘               └──────────┘               └────┬────┘
                                  ↑                          │
                                  │         sleep()/wait()   │
                                  │        ┌─────────────────↓──┐
                                  └────────│ Blocked/Waiting    │
                                  notify() └────────────────────┘
                                                             │
                                               run() ends   │
                                            ┌────────────────↓──┐
                                            │   Terminated/Dead │
                                            └───────────────────┘
```

1. **New:** Thread object is created (`new Thread()`), not yet started.
2. **Runnable:** `start()` is invoked. Thread is ready but waiting for CPU.
3. **Running:** Thread scheduler picks it; `run()` executes.
4. **Blocked/Waiting:** Thread is waiting for a resource, `sleep()`, or `wait()`.
5. **Terminated (Dead):** `run()` completes or exception occurs.

**Creating Threads — Two Methods:**

**Method 1: Extending Thread class**
```java
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(getName() + ": " + i);
            try { Thread.sleep(500); }
            catch (InterruptedException e) { System.out.println(e); }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        t1.start();  // Starts thread, calls run()
        t2.start();
    }
}
```

**Method 2: Implementing Runnable interface**
```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println(Thread.currentThread().getName() + " running");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}
```

**Important Thread Methods:** `start()`, `run()`, `sleep(ms)`, `join()`, `yield()`, `isAlive()`, `setPriority()`, `getName()`.

---

### Q5. (b) Distinguish between method overloading and method overriding with suitable example. [7 marks]

**Method Overloading (Compile-Time Polymorphism):**
- Defining **multiple methods** with the **same name** but **different parameter lists** in the **same class**.
- Resolved at **compile time** by the compiler.

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }
    int add(int a, int b, int c) {  // Different number of params
        return a + b + c;
    }
    double add(double a, double b) {  // Different type of params
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 10));        // Calls add(int, int) → 15
        System.out.println(calc.add(5, 10, 15));    // Calls add(int, int, int) → 30
        System.out.println(calc.add(2.5, 3.5));     // Calls add(double, double) → 6.0
    }
}
```

**Method Overriding (Runtime Polymorphism):**
- A **subclass provides its own implementation** of a method already defined in the **parent class**.
- Must have the **same name, same parameters, and same return type**.
- Resolved at **runtime** by the JVM based on the actual object type.

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {  // Same name, same params — overriding
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a;
        a = new Dog();
        a.sound();  // Output: Dog barks (runtime decision)
        a = new Cat();
        a.sound();  // Output: Cat meows (runtime decision)
    }
}
```

**Difference between Method Overloading and Method Overriding:**

| Feature | Method Overloading | Method Overriding |
|---------|-------------------|-------------------|
| **Definition** | Same method name, different parameters in same class | Same method name and parameters in parent-child classes |
| **Class Requirement** | Within the **same** class | Requires **inheritance** (two classes) |
| **Parameters** | Must be **different** (number/type/order) | Must be **exactly same** |
| **Return Type** | Can be different | Must be same (or covariant) |
| **Polymorphism** | Compile-Time (Static) | Runtime (Dynamic) |
| **Binding** | Early Binding | Late Binding |
| **Access Modifier** | No restrictions | Cannot reduce visibility (e.g., public → private ❌) |
| **Static Methods** | Can be overloaded | Cannot be overridden |
| **Private Methods** | Can be overloaded | Cannot be overridden |
| **`@Override`** | Not used | Used |
| **Performance** | Faster | Slightly slower |

---

### Q6. (a) What is a layout manager? What is the difference between Scrollbar and a JScrollPane? Explain with example. [7 marks]

**Layout Manager:**

A Layout Manager is an object that controls the **size and position** of components within a container in Java GUI (AWT/Swing). Instead of manually setting coordinates, layout managers automatically arrange components as the window is resized.

**Types of Layout Managers:**

| Layout Manager | Description |
|---------------|-------------|
| `FlowLayout` | Components arranged left to right, wrapping to next line (default for JPanel) |
| `BorderLayout` | Divides container into 5 regions: NORTH, SOUTH, EAST, WEST, CENTER (default for JFrame) |
| `GridLayout` | Arranges components in a grid of rows and columns |
| `BoxLayout` | Arranges components in a single row or column |
| `CardLayout` | Stacks components like cards; only one visible at a time |
| `GridBagLayout` | Most flexible; components can span multiple cells |

**Example:**
```java
import javax.swing.*;
import java.awt.*;

public class LayoutDemo extends JFrame {
    LayoutDemo() {
        setLayout(new FlowLayout());  // Set layout manager
        add(new JButton("Button 1"));
        add(new JButton("Button 2"));
        add(new JButton("Button 3"));
        setSize(300, 200);
        setVisible(true);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new LayoutDemo();
    }
}
```

**Difference between Scrollbar and JScrollPane:**

| Feature | Scrollbar (AWT) | JScrollPane (Swing) |
|---------|-----------------|---------------------|
| **Package** | `java.awt.Scrollbar` | `javax.swing.JScrollPane` |
| **Type** | AWT component (heavyweight) | Swing component (lightweight) |
| **Purpose** | A standalone scrollbar control; must manually handle scroll events | A container that automatically provides scrollbars for its child component |
| **Usage** | Used as an independent UI element for selecting values in a range | Wraps a component (like JTextArea, JTable) and adds scrollbars automatically |
| **Scrollbar Management** | Must manually write scroll logic | Scrollbars appear/disappear automatically based on content size |
| **Orientation** | `Scrollbar.HORIZONTAL` or `Scrollbar.VERTICAL` | Both horizontal and vertical by default |

**JScrollPane Example:**
```java
import javax.swing.*;

public class ScrollDemo extends JFrame {
    ScrollDemo() {
        JTextArea textArea = new JTextArea(20, 30);
        JScrollPane scrollPane = new JScrollPane(textArea);  // Auto scrollbars
        add(scrollPane);
        setSize(400, 300);
        setVisible(true);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new ScrollDemo();
    }
}
```

---

### Q6. (b) What is Java Database Connectivity (JDBC)? Explain different JDBC drivers in Java. [7 marks]

**JDBC (Java Database Connectivity):**

JDBC is a **Java API** that enables Java programs to interact with **relational databases**. It provides methods for querying and updating data in a database using SQL.

**JDBC Architecture:**
```
Java Application → JDBC API → JDBC Driver Manager → JDBC Driver → Database
```

**Steps to Connect using JDBC:**
```java
import java.sql.*;

public class JDBCExample {
    public static void main(String[] args) {
        try {
            // 1. Load driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 2. Establish connection
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");

            // 3. Create statement
            Statement stmt = con.createStatement();

            // 4. Execute query
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");

            // 5. Process results
            while (rs.next()) {
                System.out.println(rs.getInt(1) + " " + rs.getString(2));
            }

            // 6. Close connection
            con.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```

**Four Types of JDBC Drivers:**

**Type 1: JDBC-ODBC Bridge Driver**
- Uses ODBC driver to connect to the database
- Converts JDBC calls to ODBC calls
- Requires ODBC driver installed on client machine
- **Disadvantage:** Platform dependent, slow performance, removed in Java 8

**Type 2: Native API Driver (Partially Java)**
- Converts JDBC calls to database-specific native API calls
- Uses native libraries of the database (written in C/C++)
- **Advantage:** Better performance than Type 1
- **Disadvantage:** Native library must be installed on client machine; not portable

**Type 3: Network Protocol Driver (Middleware)**
- Uses a middle-tier server that converts JDBC calls to database-specific protocol
- Pure Java on client side; middleware handles the conversion
- **Advantage:** No client-side library needed, supports multiple databases
- **Disadvantage:** Requires middleware server setup

**Type 4: Thin Driver (Pure Java)**
- Converts JDBC calls **directly** into database-specific network protocol
- Written entirely in Java — no native libraries needed
- **Advantage:** Best performance, platform independent, no extra software
- **Disadvantage:** Driver is database-specific
- **Example:** MySQL Connector/J, Oracle Thin Driver

| Feature | Type 1 | Type 2 | Type 3 | Type 4 |
|---------|--------|--------|--------|--------|
| **Pure Java** | ❌ | ❌ | ✅ (client) | ✅ |
| **Performance** | Slowest | Moderate | Good | Best |
| **Platform Independent** | ❌ | ❌ | ✅ | ✅ |
| **Usage** | Obsolete | Rare | Enterprise | Most Common |

---

### Q7. (a) What is an event? Discuss various models available for event handling in Java. [7 marks]

**Event:**

An event is an **object** that describes a **state change** in a source component. It is generated when the user interacts with GUI components (clicking a button, typing in a text field, moving the mouse, etc.).

**Event Examples:**
- Clicking a button → `ActionEvent`
- Typing in a text field → `KeyEvent`
- Moving the mouse → `MouseEvent`
- Closing a window → `WindowEvent`

**Event Handling Models in Java:**

**1. Delegation Event Model (Modern — Java 1.1+):**

This is the **current standard** model used in Java. It has three components:

- **Event Source:** The GUI component that generates an event (e.g., `JButton`, `JTextField`)
- **Event Object:** The object created when the event occurs (e.g., `ActionEvent`, `MouseEvent`)
- **Event Listener:** The interface that receives and handles the event (e.g., `ActionListener`, `MouseListener`)

**How it works:**
1. The listener **registers** itself with the source using `addXxxListener()`
2. When the user interacts, the source creates an **Event object**
3. The source **delegates** the event to the registered listener
4. The listener's handler method is invoked (e.g., `actionPerformed()`)

```java
import javax.swing.*;
import java.awt.event.*;

public class EventDemo extends JFrame implements ActionListener {
    JButton btn;

    EventDemo() {
        btn = new JButton("Click Me");
        btn.addActionListener(this);  // Register listener
        add(btn);
        setSize(300, 200);
        setVisible(true);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    // Event handler method
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button was clicked!");
    }

    public static void main(String[] args) {
        new EventDemo();
    }
}
```

**2. Hierarchical Event Model (Old — Java 1.0, Deprecated):**
- Events were passed up the **component hierarchy** (child → parent → grandparent)
- Any component in the hierarchy could handle or consume the event
- **Disadvantage:** Events were delivered to components that didn't need them, wasting CPU cycles
- Replaced by the Delegation model for better performance and flexibility

**Common Event Listener Interfaces:**

| Listener Interface | Handler Method | Event Type |
|-------------------|----------------|------------|
| `ActionListener` | `actionPerformed()` | Button clicks |
| `MouseListener` | `mouseClicked()`, `mousePressed()`, etc. | Mouse actions |
| `KeyListener` | `keyPressed()`, `keyReleased()`, `keyTyped()` | Keyboard input |
| `WindowListener` | `windowClosing()`, `windowOpened()`, etc. | Window events |
| `ItemListener` | `itemStateChanged()` | Checkbox, combo box |

---

### Q7. (b) What is meant by controls? Explain different types of controls available in Abstract Window Toolkit (AWT). [7 marks]

**Controls:**

Controls are **GUI components** that allow the user to interact with the application. They are visual elements like buttons, text fields, labels, checkboxes, etc. In Java, AWT controls are part of the `java.awt` package and are **heavyweight** (they rely on native OS components).

**Types of AWT Controls:**

**1. Label** — Displays read-only text
```java
Label l = new Label("Enter Name:");
```

**2. Button** — A clickable button that triggers an action
```java
Button btn = new Button("Submit");
btn.addActionListener(e -> System.out.println("Clicked"));
```

**3. TextField** — Single-line text input
```java
TextField tf = new TextField(20);  // 20-column width
String text = tf.getText();        // Get entered text
```

**4. TextArea** — Multi-line text input
```java
TextArea ta = new TextArea(5, 30);  // 5 rows, 30 columns
```

**5. Checkbox** — Toggle selection (checked/unchecked)
```java
Checkbox cb1 = new Checkbox("Java");
Checkbox cb2 = new Checkbox("Python");
boolean isChecked = cb1.getState();
```

**6. CheckboxGroup (Radio Buttons)** — Only one can be selected at a time
```java
CheckboxGroup group = new CheckboxGroup();
Checkbox male = new Checkbox("Male", group, true);
Checkbox female = new Checkbox("Female", group, false);
```

**7. Choice (Dropdown List)** — Single selection from a drop-down list
```java
Choice choice = new Choice();
choice.add("Red");
choice.add("Green");
choice.add("Blue");
String selected = choice.getSelectedItem();
```

**8. List** — Displays a scrollable list of items with single or multiple selection
```java
List list = new List(4, true);  // 4 visible rows, multi-select
list.add("Item 1");
list.add("Item 2");
list.add("Item 3");
```

**9. Scrollbar** — Provides a scrollbar for selecting a value in a range
```java
Scrollbar sb = new Scrollbar(Scrollbar.HORIZONTAL, 0, 10, 0, 100);
```

**Complete AWT Example:**
```java
import java.awt.*;

public class AWTControls extends Frame {
    AWTControls() {
        setLayout(new FlowLayout());
        add(new Label("Name:"));
        add(new TextField(15));
        add(new Button("Submit"));
        add(new Checkbox("Agree"));

        Choice c = new Choice();
        c.add("CSE"); c.add("ECE"); c.add("ME");
        add(c);

        setSize(400, 300);
        setVisible(true);
    }

    public static void main(String[] args) {
        new AWTControls();
    }
}
```

---

### Q8. Write short notes on the following (*any two*): [7 × 2 = 14 marks]

**(a) Dynamic Method Dispatch:**

Dynamic Method Dispatch is the mechanism by which a call to an **overridden method** is resolved at **runtime** rather than compile time. It is the basis of **Runtime Polymorphism** in Java.

- When an overridden method is called through a **superclass reference**, Java determines which version of the method to call based on the **actual object type** (not the reference type).
- Also called **late binding** or **dynamic binding**.

```java
class Animal {
    void sound() { System.out.println("Animal sound"); }
}
class Dog extends Animal {
    void sound() { System.out.println("Dog barks"); }
}
class Cat extends Animal {
    void sound() { System.out.println("Cat meows"); }
}

public class Main {
    public static void main(String[] args) {
        Animal a;        // Superclass reference
        a = new Dog();   // Points to Dog object
        a.sound();       // Output: Dog barks (resolved at runtime)
        a = new Cat();   // Points to Cat object
        a.sound();       // Output: Cat meows (resolved at runtime)
    }
}
```

**Key Point:** The reference type determines **which methods can be called**, but the object type determines **which implementation is executed**.

---

**(b) Iterator Class:**

An Iterator is an interface in `java.util` package that provides a way to **traverse (iterate) through a collection** of elements one by one, without exposing the underlying data structure.

**Methods of Iterator:**
- `hasNext()` — Returns `true` if there are more elements
- `next()` — Returns the next element in the collection
- `remove()` — Removes the last element returned by the iterator

```java
import java.util.*;

public class IteratorDemo {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Python");
        list.add("C++");

        Iterator<String> it = list.iterator();
        while (it.hasNext()) {
            String val = it.next();
            System.out.println(val);
            if (val.equals("Python")) {
                it.remove();  // Safe removal during iteration
            }
        }
        System.out.println("After removal: " + list);
    }
}
```

**Advantages:**
- Universal way to traverse any Collection (List, Set, Queue)
- Allows safe removal of elements during iteration (unlike for-each loop)
- Follows the **Iterator Design Pattern**

---

**(c) Thread Synchronization:**

Synchronization is the mechanism that controls the **access of multiple threads to shared resources** to prevent **race conditions** and **data inconsistency**.

When multiple threads access shared data simultaneously without synchronization, the results can be unpredictable.

**Achieved using the `synchronized` keyword:**

```java
class Counter {
    int count = 0;

    // Synchronized method — only one thread can execute at a time
    synchronized void increment() {
        count++;
    }
}

class MyThread extends Thread {
    Counter c;
    MyThread(Counter c) { this.c = c; }
    public void run() {
        for (int i = 0; i < 1000; i++) {
            c.increment();
        }
    }
}

public class SyncDemo {
    public static void main(String[] args) throws InterruptedException {
        Counter c = new Counter();
        MyThread t1 = new MyThread(c);
        MyThread t2 = new MyThread(c);
        t1.start(); t2.start();
        t1.join(); t2.join();
        System.out.println("Count: " + c.count);  // Always 2000 with synchronized
    }
}
```

**Types:** Synchronized methods, Synchronized blocks, Static synchronization.
**Concepts:** Monitor lock (intrinsic lock), `wait()`, `notify()`, `notifyAll()`.

---

**(d) TCP/IP Server Socket:**

TCP/IP (Transmission Control Protocol/Internet Protocol) sockets enable **reliable, ordered, connection-oriented communication** between two computers over a network.

**Java provides two classes for TCP socket programming:**
- `Socket` — Used by **client** to establish connection
- `ServerSocket` — Used by **server** to listen for incoming connections

**Server Example:**
```java
import java.io.*;
import java.net.*;

public class Server {
    public static void main(String[] args) throws Exception {
        ServerSocket ss = new ServerSocket(6666);  // Listen on port 6666
        System.out.println("Server waiting for client...");

        Socket s = ss.accept();  // Accept client connection
        System.out.println("Client connected!");

        DataInputStream dis = new DataInputStream(s.getInputStream());
        String msg = dis.readUTF();
        System.out.println("Client says: " + msg);

        DataOutputStream dos = new DataOutputStream(s.getOutputStream());
        dos.writeUTF("Hello from Server!");

        ss.close();
    }
}
```

**Client Example:**
```java
import java.io.*;
import java.net.*;

public class Client {
    public static void main(String[] args) throws Exception {
        Socket s = new Socket("localhost", 6666);

        DataOutputStream dos = new DataOutputStream(s.getOutputStream());
        dos.writeUTF("Hello from Client!");

        DataInputStream dis = new DataInputStream(s.getInputStream());
        String reply = dis.readUTF();
        System.out.println("Server says: " + reply);

        s.close();
    }
}
```

**Key Features:** Connection-oriented, reliable delivery, bi-directional communication, stream-based (ordered bytes).

---

## Subjective Questions & Solutions (2022)

### Q2. (a) What are the various data types supported by Java? Explain type casting methods in Java. [7 marks]

**Data Types in Java:**

Java supports two categories of data types:

**1. Primitive Data Types (8 types):**

| Data Type | Size | Default Value | Range / Description |
|-----------|------|---------------|---------------------|
| `byte` | 1 byte | 0 | -128 to 127 |
| `short` | 2 bytes | 0 | -32,768 to 32,767 |
| `int` | 4 bytes | 0 | -2³¹ to 2³¹ - 1 |
| `long` | 8 bytes | 0L | -2⁶³ to 2⁶³ - 1 |
| `float` | 4 bytes | 0.0f | Up to 7 decimal digits |
| `double` | 8 bytes | 0.0d | Up to 15 decimal digits |
| `char` | 2 bytes | '\u0000' | Unicode character (0 to 65,535) |
| `boolean` | 1 bit | false | `true` or `false` |

**2. Non-Primitive (Reference) Data Types:**
- **Class** — Blueprint of objects (e.g., `String`, `Scanner`)
- **Interface** — Abstract type with method signatures
- **Array** — Collection of similar data types (e.g., `int[]`)

**Type Casting in Java:**

Type casting is the process of converting one data type to another.

**1. Implicit Type Casting (Widening) — Automatic:**
- Converts a smaller type to a larger type automatically
- No data loss occurs
- Order: `byte → short → int → long → float → double`

```java
int a = 100;
long b = a;      // int to long (automatic)
float c = b;     // long to float (automatic)
double d = c;    // float to double (automatic)
System.out.println(d);  // Output: 100.0
```

**2. Explicit Type Casting (Narrowing) — Manual:**
- Converts a larger type to a smaller type manually
- May cause **data loss** (truncation)
- Requires explicit cast operator `(type)`

```java
double x = 9.78;
int y = (int) x;     // double to int (manual) — decimal part lost
System.out.println(y);  // Output: 9

long l = 100000L;
byte b = (byte) l;   // long to byte — data loss due to range
System.out.println(b);  // Output: -96 (overflow)
```

**3. Type Promotion in Expressions:**
```java
byte a = 50;
byte b = 30;
int result = a * b;  // Automatically promoted to int in expressions
```

---

### Q2. (b) Explain OOPs principle used in Java programming. [7 marks]

**Four Main OOP Principles in Java:**

**1. Encapsulation:**
- **Wrapping data (variables) and methods** that operate on the data into a single unit (class).
- Data is hidden using `private` access modifier; accessed through public getters/setters.
- Provides **data hiding** and **data protection**.

```java
class Student {
    private String name;  // Hidden data
    public void setName(String n) { name = n; }    // Setter
    public String getName() { return name; }         // Getter
}
```

**2. Abstraction:**
- **Hiding implementation details** and showing only essential features.
- Achieved through `abstract` classes and `interface`.
- Reduces complexity for the user.

```java
abstract class Shape {
    abstract double area();  // Only WHAT, not HOW
}
class Circle extends Shape {
    double r;
    Circle(double r) { this.r = r; }
    double area() { return 3.14 * r * r; }  // HOW is defined here
}
```

**3. Inheritance:**
- A class **acquires properties and methods** of another class.
- Promotes **code reusability** and establishes IS-A relationship.
- Uses `extends` keyword.

```java
class Animal {
    void eat() { System.out.println("Eating"); }
}
class Dog extends Animal {  // Dog IS-A Animal
    void bark() { System.out.println("Barking"); }
}
// Dog inherits eat() from Animal
```

**4. Polymorphism:**
- One entity takes **many forms**.
- **Compile-time polymorphism** — Method Overloading (same name, different parameters)
- **Runtime polymorphism** — Method Overriding (same name, same parameters in parent-child)

```java
// Overloading (Compile-time)
class Calc {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

// Overriding (Runtime)
class Animal {
    void sound() { System.out.println("Sound"); }
}
class Cat extends Animal {
    void sound() { System.out.println("Meow"); }  // Overridden
}
```

---

### Q3. (a) Discuss the difference between class and object with example. What is the purpose of constructor in Java? [7 marks]

**Class:**
- A class is a **blueprint or template** that defines the properties (variables) and behaviors (methods) of objects.
- It is a **logical entity** — no memory is allocated until an object is created.
- Defined using the `class` keyword.

**Object:**
- An object is a **real-world instance** of a class.
- It is a **physical entity** — memory is allocated on the heap when created using `new`.
- Each object has its own copy of instance variables.

**Difference between Class and Object:**

| Feature | Class | Object |
|---------|-------|--------|
| **Definition** | Blueprint/template for creating objects | Instance of a class |
| **Memory** | No memory allocated | Memory allocated on heap |
| **Creation** | Defined using `class` keyword | Created using `new` keyword |
| **Nature** | Logical entity | Physical entity |
| **Existence** | Defined once | Multiple objects can be created |
| **Declaration** | `class Student { }` | `Student s = new Student();` |
| **Members** | Contains variable declarations and method definitions | Contains actual values and can invoke methods |

**Example:**
```java
// Class — Blueprint
class Car {
    String brand;
    int speed;

    void display() {
        System.out.println(brand + " - Speed: " + speed);
    }
}

public class Main {
    public static void main(String[] args) {
        // Objects — Instances of Car class
        Car c1 = new Car();
        c1.brand = "Toyota"; c1.speed = 180;

        Car c2 = new Car();
        c2.brand = "Honda"; c2.speed = 200;

        c1.display();  // Toyota - Speed: 180
        c2.display();  // Honda - Speed: 200
    }
}
```

**Purpose of Constructor in Java:**

A constructor is a special method used to **initialize objects** at the time of creation.

**Purposes:**
1. **Initialization:** Sets initial values for instance variables
2. **Memory Allocation:** Allocates memory when called with `new`
3. **Automatic Invocation:** Called automatically when object is created
4. **Overloading:** Multiple constructors provide flexible initialization

```java
class Student {
    String name;
    int age;

    // Constructor — initializes the object
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
Student s = new Student("Amit", 20);  // Constructor called automatically
```

---

### Q3. (b) Define a class Circle with appropriate data members and two methods area() and circum() to calculate the area and circumference of the circle. Also create a constructor to initialize the radius of the circle. Finally create a main class to find the area and circumference of the circle. [7 marks]

```java
import java.util.Scanner;

class Circle {
    double radius;
    final double PI = 3.14159;

    // Constructor to initialize the radius
    Circle(double radius) {
        this.radius = radius;
    }

    // Method to calculate area
    double area() {
        return PI * radius * radius;
    }

    // Method to calculate circumference
    double circum() {
        return 2 * PI * radius;
    }

    // Method to display details
    void display() {
        System.out.println("Radius: " + radius);
        System.out.println("Area: " + area());
        System.out.println("Circumference: " + circum());
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter radius of the circle: ");
        double r = sc.nextDouble();

        // Creating Circle object using constructor
        Circle c = new Circle(r);

        // Displaying area and circumference
        c.display();

        sc.close();
    }
}
```

**Output:**
```
Enter radius of the circle: 7
Radius: 7.0
Area: 153.93791
Circumference: 43.98226
```

**Explanation:**
- `Circle` class has `radius` as data member and `PI` as a constant
- Constructor `Circle(double radius)` initializes the radius
- `area()` method returns π × r²
- `circum()` method returns 2 × π × r
- In `main()`, user inputs the radius, Circle object is created, and results are displayed

---

### Q4. (a) What is an exception? What are the various steps involved in exception handling? [7 marks]

**Exception:**

An exception is an **unwanted or unexpected event** that occurs during the execution of a program and **disrupts the normal flow** of instructions. It is an object generated by the JVM or manually thrown by the programmer.

**Exception Hierarchy:**
```
Throwable
├── Error (serious, unrecoverable)
│   ├── OutOfMemoryError
│   ├── StackOverflowError
│   └── VirtualMachineError
└── Exception (recoverable)
    ├── Checked Exceptions (compile-time)
    │   ├── IOException
    │   ├── SQLException
    │   └── FileNotFoundException
    └── Unchecked Exceptions (runtime)
        ├── ArithmeticException
        ├── NullPointerException
        └── ArrayIndexOutOfBoundsException
```

**Steps Involved in Exception Handling:**

**Step 1: Identify risky code** — Enclose code that might throw an exception inside a `try` block.

**Step 2: Handle the exception** — Use `catch` block(s) to handle specific exceptions.

**Step 3: Cleanup resources** — Use `finally` block to release resources (always executes).

**Step 4: Declare exceptions** — Use `throws` keyword in the method signature to declare checked exceptions.

**Step 5: Throw exceptions** — Use `throw` keyword to explicitly throw an exception.

**Exception Handling Keywords:**

| Keyword | Purpose |
|---------|---------|
| `try` | Encloses code that may throw exception |
| `catch` | Handles the exception |
| `finally` | Always executes (cleanup code) |
| `throw` | Explicitly throws an exception |
| `throws` | Declares exceptions in method signature |

**Example:**
```java
public class ExceptionDemo {
    public static void main(String[] args) {
        try {
            int[] arr = {1, 2, 3};
            System.out.println(arr[5]);  // ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index out of bounds: " + e.getMessage());
        } catch (Exception e) {
            System.out.println("General exception: " + e.getMessage());
        } finally {
            System.out.println("Finally block always executes");
        }
        System.out.println("Program continues normally...");
    }
}
```

**Output:**
```
Array index out of bounds: Index 5 out of bounds for length 3
Finally block always executes
Program continues normally...
```

---

### Q4. (b) Write an example of try and catch block to handle multiple exceptions. [7 marks]

When multiple types of exceptions can occur, we can use **multiple catch blocks** with a single `try` block. Each catch block handles a specific type of exception.

**Rules:**
- More specific exceptions should come **before** general ones
- Once a catch block handles an exception, remaining catch blocks are skipped
- `Exception` (most general) should always be the last catch block

```java
import java.util.Scanner;

public class MultipleCatchDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        try {
            System.out.print("Enter a number: ");
            String input = sc.nextLine();

            // May throw NumberFormatException
            int num = Integer.parseInt(input);

            // May throw ArithmeticException
            int result = 100 / num;
            System.out.println("Result: " + result);

            // May throw ArrayIndexOutOfBoundsException
            int[] arr = {10, 20, 30};
            System.out.println("Element: " + arr[num]);

            // May throw NullPointerException
            String str = null;
            System.out.println(str.length());

        } catch (NumberFormatException e) {
            System.out.println("Error: Invalid number format! " + e.getMessage());

        } catch (ArithmeticException e) {
            System.out.println("Error: Division by zero! " + e.getMessage());

        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Error: Array index out of bounds! " + e.getMessage());

        } catch (NullPointerException e) {
            System.out.println("Error: Null pointer! " + e.getMessage());

        } catch (Exception e) {
            // General catch — catches any remaining exception
            System.out.println("Error: " + e.getMessage());

        } finally {
            System.out.println("Program cleanup complete.");
            sc.close();
        }

        System.out.println("Program continues after exception handling.");
    }
}
```

**Test Runs:**
```
Input: "abc" → Error: Invalid number format! For input string: "abc"
Input: 0     → Error: Division by zero! / by zero
Input: 5     → Result: 20 → Error: Array index out of bounds! Index 5 out of bounds for length 3
Input: 1     → Result: 100 → Element: 20 → Error: Null pointer! null
```

**Multi-Catch (Java 7+):**
```java
try {
    // code
} catch (ArithmeticException | NumberFormatException e) {
    System.out.println("Error: " + e.getMessage());
}
```

---

### Q5. (a) What are packages? How are packages declared and defined in Java programming language? Write the advantages of using packages in Java programs. [7 marks]

**Packages:**

A package is a **namespace** that organizes a group of related classes and interfaces into a single directory structure. It helps avoid **naming conflicts** and provides **access control**.

**Types of Packages:**
1. **Built-in (Predefined) Packages:**
   - `java.lang` — Core classes (String, Math, System) — auto-imported
   - `java.util` — Collections, Scanner, Date
   - `java.io` — Input/Output streams
   - `java.sql` — Database connectivity
   - `java.net` — Networking classes
   - `javax.swing` — GUI components

2. **User-Defined Packages:**
   - Created by the programmer to organize their own classes

**Declaring and Defining a Package:**

**Step 1:** Use the `package` keyword as the first statement in the file:
```java
// File: mypackage/Student.java
package mypackage;

public class Student {
    public String name;
    public int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}
```

**Step 2:** Compile with directory structure:
```
javac -d . Student.java
```
This creates: `mypackage/Student.class`

**Step 3:** Import and use the package:
```java
// File: Main.java
import mypackage.Student;  // Import the class

public class Main {
    public static void main(String[] args) {
        Student s = new Student("Amit", 20);
        s.display();
    }
}
```

**Sub-Packages:**
```java
package mypackage.subpackage;  // Sub-package declaration
```

**Advantages of Using Packages:**

1. **Namespace Management:** Prevents naming conflicts — two classes with the same name can exist in different packages.
   ```java
   mypackage1.Student s1;
   mypackage2.Student s2;  // No conflict!
   ```

2. **Access Control:** Package-level access (default modifier) restricts visibility to classes within the same package, enhancing security.

3. **Code Organization:** Groups related classes together, making the project structure logical and clean.

4. **Reusability:** Packages can be imported and reused across different projects.

5. **Easy Maintenance:** Easier to locate, modify, and debug classes when they are organized in packages.

6. **Modularity:** Encourages modular programming by separating concerns into different packages.

---

### Q5. (b) Explain the use of super keyword in Java with suitable example. [7 marks]

**The `super` Keyword:**

The `super` keyword in Java is a reference variable used to refer to the **immediate parent class** object. It is used in three contexts:

**1. To access parent class variables (when hidden by child class):**

When a child class has a variable with the same name as the parent class, `super` is used to access the parent's variable.

```java
class Animal {
    String type = "Animal";
}

class Dog extends Animal {
    String type = "Dog";

    void display() {
        System.out.println("Child type: " + type);         // Dog
        System.out.println("Parent type: " + super.type);   // Animal
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.display();
    }
}
```
**Output:**
```
Child type: Dog
Parent type: Animal
```

**2. To invoke parent class methods (when overridden):**

When a child class overrides a parent class method, `super` can call the parent's version.

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    void sound() {
        super.sound();  // Calls parent's sound()
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound();
    }
}
```
**Output:**
```
Animal makes a sound
Dog barks
```

**3. To invoke parent class constructor:**

`super()` is used to call the parent class constructor from the child class constructor. It must be the **first statement** in the child constructor.

```java
class Animal {
    String name;

    Animal(String name) {
        this.name = name;
        System.out.println("Animal constructor: " + name);
    }
}

class Dog extends Animal {
    String breed;

    Dog(String name, String breed) {
        super(name);  // Calls parent's constructor — MUST be first line
        this.breed = breed;
        System.out.println("Dog constructor: " + breed);
    }

    void display() {
        System.out.println("Name: " + name + ", Breed: " + breed);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog("Tommy", "Labrador");
        d.display();
    }
}
```
**Output:**
```
Animal constructor: Tommy
Dog constructor: Labrador
Name: Tommy, Breed: Labrador
```

**Summary:**

| Usage | Syntax | Purpose |
|-------|--------|---------|
| Access parent variable | `super.variableName` | When child has same-named variable |
| Call parent method | `super.methodName()` | When child overrides parent method |
| Call parent constructor | `super(args)` | Must be first line in child constructor |

---

### Q6. (a) What is an Applet? Explain the lifecycle of an Applet. [7 marks]

**Applet:**

An Applet is a **small Java program** that runs inside a web browser or an applet viewer. It is a subclass of `java.applet.Applet` and is embedded in HTML pages.

> **Note:** Applets are **deprecated** since Java 9 and **removed** in Java 11. However, they are still asked in exams.

**Key Features:**
- Applets don't have a `main()` method
- They run in a browser's sandbox environment (restricted access)
- They are event-driven programs

**Applet Lifecycle:**

An applet goes through **five lifecycle methods**, called by the browser/applet viewer:

```
          ┌────────┐
          │ init() │  ← Called once when applet is first loaded
          └───┬────┘
              ↓
          ┌─────────┐
          │ start() │  ← Called each time applet becomes active
          └───┬─────┘
              ↓
          ┌──────────────┐
          │ paint(Graphics)│  ← Called to draw/redraw the applet
          └───┬──────────┘
              ↓
          ┌────────┐
          │ stop() │  ← Called when applet becomes inactive
          └───┬────┘
              ↓
          ┌───────────┐
          │ destroy() │  ← Called once when applet is removed
          └───────────┘
```

| Method | When Called | Purpose |
|--------|-----------|---------|
| `init()` | Once, when applet is first loaded | Initialize variables, set layout, load resources |
| `start()` | After `init()` and each time applet is revisited | Start animations, threads |
| `paint(Graphics g)` | Whenever applet needs to be drawn/redrawn | Draw shapes, text, images on screen |
| `stop()` | When user leaves the page or minimizes browser | Pause running threads, animations |
| `destroy()` | When applet is permanently removed | Release all resources, cleanup |

**Example:**
```java
import java.applet.Applet;
import java.awt.Graphics;

/*
<applet code="MyApplet" width="300" height="200">
</applet>
*/

public class MyApplet extends Applet {
    String message;

    public void init() {
        message = "Applet Initialized";
        System.out.println("init() called");
    }

    public void start() {
        message = "Applet Started";
        System.out.println("start() called");
    }

    public void paint(Graphics g) {
        g.drawString(message, 50, 100);
        System.out.println("paint() called");
    }

    public void stop() {
        System.out.println("stop() called");
    }

    public void destroy() {
        System.out.println("destroy() called");
    }
}
```

---

### Q6. (b) What is Java Database Connectivity (JDBC)? Explain the role of JDBC driver. [7 marks]

**JDBC (Java Database Connectivity):**

JDBC is a **standard Java API** that provides a set of interfaces and classes for connecting Java applications to relational databases. It enables Java programs to execute SQL queries, retrieve results, and update data.

**JDBC Architecture:**
```
Java Application
       ↓
   JDBC API (java.sql package)
       ↓
   JDBC Driver Manager
       ↓
   JDBC Driver
       ↓
   Database (MySQL, Oracle, PostgreSQL, etc.)
```

**Key JDBC Interfaces:**
- `Connection` — Establishes connection to database
- `Statement` — Executes SQL queries
- `PreparedStatement` — Executes parameterized queries (prevents SQL injection)
- `ResultSet` — Stores the results of a query
- `DriverManager` — Manages JDBC drivers

**JDBC Example:**
```java
import java.sql.*;

public class JDBCDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the JDBC driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 2. Establish connection
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");

            // 3. Create statement
            Statement stmt = con.createStatement();

            // 4. Execute query
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");

            // 5. Process results
            while (rs.next()) {
                System.out.println(rs.getInt("id") + " - " + rs.getString("name"));
            }

            // 6. Close connection
            rs.close();
            stmt.close();
            con.close();

        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Role of JDBC Driver:**

The JDBC driver acts as a **translator** between the Java application and the database. It converts JDBC method calls into database-specific protocol calls.

**Four Types of JDBC Drivers:**

| Type | Name | Description | Performance |
|------|------|-------------|-------------|
| Type 1 | JDBC-ODBC Bridge | Converts JDBC → ODBC calls; platform dependent | Slowest |
| Type 2 | Native API | Uses database-specific native C/C++ libraries | Moderate |
| Type 3 | Network Protocol | Uses middleware server; pure Java on client | Good |
| Type 4 | Thin Driver | Pure Java; directly converts to DB protocol | Best |

**Role of Driver:**
1. **Translation:** Converts Java JDBC calls to database-specific protocol
2. **Connection Management:** Establishes and manages database connections
3. **Query Execution:** Sends SQL queries to the database
4. **Result Processing:** Converts database results into Java-readable `ResultSet`
5. **Error Handling:** Translates database errors into Java exceptions (`SQLException`)

---

### Q7. (a) What is layout manager? Explain different types of layout managers available in Java Swing with example. [7 marks]

**Layout Manager:**

A Layout Manager is a Java object that automatically controls the **size and arrangement** of components within a container. It eliminates the need for manual positioning, ensuring that the GUI looks consistent across different platforms and screen sizes.

**Types of Layout Managers:**

**1. FlowLayout** (Default for `JPanel`)
- Arranges components **left-to-right**, wrapping to the next line when space runs out
```java
JPanel panel = new JPanel(new FlowLayout());
panel.add(new JButton("1"));
panel.add(new JButton("2"));
panel.add(new JButton("3"));
```

**2. BorderLayout** (Default for `JFrame`)
- Divides the container into **5 regions**: NORTH, SOUTH, EAST, WEST, CENTER
```java
JFrame f = new JFrame();
f.setLayout(new BorderLayout());
f.add(new JButton("North"), BorderLayout.NORTH);
f.add(new JButton("South"), BorderLayout.SOUTH);
f.add(new JButton("East"), BorderLayout.EAST);
f.add(new JButton("West"), BorderLayout.WEST);
f.add(new JButton("Center"), BorderLayout.CENTER);
```

**3. GridLayout**
- Arranges components in a **grid** of equal-sized rows and columns
```java
JPanel panel = new JPanel(new GridLayout(3, 3));  // 3 rows, 3 cols
for (int i = 1; i <= 9; i++) {
    panel.add(new JButton(String.valueOf(i)));
}
```

**4. BoxLayout**
- Arranges components in a **single row or column**
```java
JPanel panel = new JPanel();
panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS));  // Vertical
panel.add(new JButton("Button 1"));
panel.add(new JButton("Button 2"));
```

**5. CardLayout**
- Components are **stacked like cards**; only one is visible at a time
```java
CardLayout cl = new CardLayout();
JPanel panel = new JPanel(cl);
panel.add(new JButton("Card 1"), "first");
panel.add(new JButton("Card 2"), "second");
cl.show(panel, "first");  // Show first card
```

**6. GridBagLayout**
- Most **flexible and complex** layout; components can span multiple rows/columns

**Complete Example:**
```java
import javax.swing.*;
import java.awt.*;

public class LayoutDemo extends JFrame {
    LayoutDemo() {
        setLayout(new BorderLayout());

        add(new JButton("NORTH"), BorderLayout.NORTH);
        add(new JButton("SOUTH"), BorderLayout.SOUTH);

        JPanel center = new JPanel(new GridLayout(2, 2));
        center.add(new JButton("1"));
        center.add(new JButton("2"));
        center.add(new JButton("3"));
        center.add(new JButton("4"));
        add(center, BorderLayout.CENTER);

        setSize(400, 300);
        setVisible(true);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new LayoutDemo();
    }
}
```

| Layout | Best For |
|--------|---------|
| FlowLayout | Toolbars, simple button panels |
| BorderLayout | Main window with header, footer, sidebar |
| GridLayout | Calculator keypads, uniform grids |
| BoxLayout | Vertical/horizontal component stacking |
| CardLayout | Wizard-style step navigation |

---

### Q7. (b) What are the differences between AWT and Swing? Explain in detail. [7 marks]

**AWT (Abstract Window Toolkit):**
- Java's **original** GUI toolkit (since JDK 1.0)
- Part of `java.awt` package
- Uses **heavyweight** components that rely on native OS resources

**Swing:**
- Java's **modern** GUI toolkit (since JDK 1.2)
- Part of `javax.swing` package
- Uses **lightweight** components that are painted entirely in Java

**Detailed Differences:**

| Feature | AWT | Swing |
|---------|-----|-------|
| **Package** | `java.awt` | `javax.swing` |
| **Component Type** | Heavyweight (uses OS-native components) | Lightweight (pure Java rendering) |
| **Look and Feel** | Varies across OS (platform-dependent appearance) | Consistent across all platforms (pluggable L&F) |
| **Performance** | Faster (native rendering) | Slightly slower (Java rendering) |
| **Components** | Limited set (Button, Label, TextField, etc.) | Rich set (JButton, JTable, JTree, JTabbedPane, etc.) |
| **MVC Support** | Does not follow MVC pattern | Built on MVC (Model-View-Controller) pattern |
| **Naming** | `Button`, `Label`, `Frame` | `JButton`, `JLabel`, `JFrame` (prefix 'J') |
| **Components Available** | ~20 basic components | ~40+ advanced components |
| **Features** | Basic GUI elements only | Icons, tooltips, borders, tabbed panes, trees, tables |
| **Memory** | More memory (OS resources for each component) | Less memory (shared Java rendering) |
| **Pluggable L&F** | Not supported | Supports multiple look and feel themes |
| **Double Buffering** | Not built-in (flickering possible) | Built-in double buffering (smooth rendering) |

**AWT Example:**
```java
import java.awt.*;

public class AWTExample extends Frame {
    AWTExample() {
        Button btn = new Button("AWT Button");  // Heavyweight
        add(btn);
        setSize(300, 200);
        setVisible(true);
    }
    public static void main(String[] args) {
        new AWTExample();
    }
}
```

**Swing Example:**
```java
import javax.swing.*;

public class SwingExample extends JFrame {
    SwingExample() {
        JButton btn = new JButton("Swing Button");  // Lightweight
        add(btn);
        setSize(300, 200);
        setVisible(true);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }
    public static void main(String[] args) {
        new SwingExample();
    }
}
```

**When to Use:**
- **AWT:** Legacy applications, simple GUIs where platform-native look is desired
- **Swing:** Modern applications, rich GUIs, cross-platform consistency

---

### Q8. Write short notes on the following (*any two*): [7 × 2 = 14 marks]

**(a) Wrapper Class:**

A wrapper class provides a way to use **primitive data types as objects**. Each primitive type has a corresponding wrapper class in the `java.lang` package.

| Primitive | Wrapper Class |
|-----------|---------------|
| `byte` | `Byte` |
| `short` | `Short` |
| `int` | `Integer` |
| `long` | `Long` |
| `float` | `Float` |
| `double` | `Double` |
| `char` | `Character` |
| `boolean` | `Boolean` |

**Why Wrapper Classes are Needed:**
1. Collections framework (e.g., `ArrayList<Integer>`) only works with objects, not primitives
2. Provide utility methods (e.g., `Integer.parseInt()`, `Integer.toString()`)
3. Allow `null` values (primitives can't be null)

**Autoboxing and Unboxing (Java 5+):**
```java
// Autoboxing: primitive → object (automatic)
int x = 10;
Integer obj = x;  // int → Integer

// Unboxing: object → primitive (automatic)
Integer obj2 = new Integer(20);
int y = obj2;  // Integer → int

// Usage in Collections
ArrayList<Integer> list = new ArrayList<>();
list.add(5);         // Autoboxing: int 5 → Integer
int val = list.get(0);  // Unboxing: Integer → int
```

**Useful Methods:**
```java
int num = Integer.parseInt("123");          // String → int
String str = Integer.toString(123);         // int → String
int max = Integer.MAX_VALUE;                // Maximum value of int
```

---

**(b) Garbage Collection:**

Garbage collection (GC) is the **automatic memory management** process in Java that identifies and removes objects that are **no longer referenced** by any part of the program, freeing up heap memory.

**How Objects Become Eligible for GC:**
1. **Nullifying the reference:**
```java
Student s = new Student();
s = null;  // Student object is now eligible for GC
```

2. **Reassigning the reference:**
```java
Student s1 = new Student("A");
Student s2 = new Student("B");
s1 = s2;  // Object "A" is now eligible for GC
```

3. **Objects created inside a method** (local scope):
```java
void createObject() {
    Student s = new Student();  // Eligible for GC after method returns
}
```

**Key Points:**
- GC runs on a **daemon thread** in the JVM
- `System.gc()` — Requests the JVM to run GC (not guaranteed)
- `finalize()` — Method called before an object is garbage collected (deprecated in Java 9)
- Java uses **Mark-and-Sweep** algorithm for garbage collection
- GC eliminates the need for manual `free()` or `delete` (unlike C/C++)

**Advantages:**
- Prevents memory leaks
- Simplifies programming (no manual deallocation)
- Automatic memory management

**Disadvantage:**
- "Stop-the-world" pauses can affect real-time applications

---

**(c) Remote Method Invocation (RMI):**

RMI is a Java API that allows a program to **invoke methods on an object located on a different JVM** (potentially on a different machine over the network). It enables distributed computing in Java.

**RMI Architecture:**
```
Client JVM                          Server JVM
┌──────────────┐                  ┌──────────────┐
│ Client Code  │                  │ Remote Object │
│      ↓       │    Network       │      ↑       │
│   Stub       │ ←─────────────→ │   Skeleton    │
└──────────────┘                  └──────────────┘
```

**Key Components:**
1. **Remote Interface** — Defines methods that can be called remotely
2. **Remote Object (Server)** — Implements the remote interface
3. **Stub** — Client-side proxy that forwards calls to the server
4. **Skeleton** — Server-side proxy that receives calls and invokes the actual method
5. **RMI Registry** — Directory service that maps names to remote objects

**Steps to Create an RMI Application:**
```java
// 1. Remote Interface
import java.rmi.*;
public interface Hello extends Remote {
    String sayHello() throws RemoteException;
}

// 2. Implementation
import java.rmi.server.*;
public class HelloImpl extends UnicastRemoteObject implements Hello {
    HelloImpl() throws RemoteException { super(); }
    public String sayHello() { return "Hello from Server!"; }
}

// 3. Server
Naming.rebind("HelloService", new HelloImpl());

// 4. Client
Hello obj = (Hello) Naming.lookup("rmi://localhost/HelloService");
System.out.println(obj.sayHello());
```

**Advantages:** Distributed computing, network transparency, object-oriented remote calls.

---

**(d) Thread Priorities:**

Every thread in Java has a **priority** that helps the thread scheduler decide which thread to execute first when multiple threads are in the Runnable state.

**Priority Range:** 1 (lowest) to 10 (highest)

**Predefined Constants:**
| Constant | Value |
|----------|-------|
| `Thread.MIN_PRIORITY` | 1 |
| `Thread.NORM_PRIORITY` | 5 (default) |
| `Thread.MAX_PRIORITY` | 10 |

**Methods:**
- `setPriority(int priority)` — Sets the thread's priority
- `getPriority()` — Returns the thread's priority

```java
class MyThread extends Thread {
    public void run() {
        System.out.println(getName() + " Priority: " + getPriority());
    }
}

public class PriorityDemo {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        MyThread t3 = new MyThread();

        t1.setName("Low");
        t1.setPriority(Thread.MIN_PRIORITY);     // Priority 1

        t2.setName("Normal");
        t2.setPriority(Thread.NORM_PRIORITY);    // Priority 5

        t3.setName("High");
        t3.setPriority(Thread.MAX_PRIORITY);     // Priority 10

        t1.start();
        t2.start();
        t3.start();
    }
}
```

**Key Points:**
- A child thread inherits the priority of its parent thread
- Higher priority threads get **more CPU time**, but this is **not guaranteed** (depends on OS scheduler)
- Thread priority is **advisory**, not mandatory — the OS makes the final scheduling decision
- Use priorities carefully; over-reliance can lead to thread starvation

