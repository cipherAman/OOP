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
    - **d. java.util (Correct)**

---

## Subjective Questions & Solutions (2024)

### 1. Need of OOP paradigm and comparison with structured programming
**Need of OOP Paradigm:**
- **Reusability:** Code can be reused through inheritance.
- **Maintainability:** Modular structure makes it easier to troubleshoot and modify.
- **Data Security:** Encapsulation and data hiding keep data safe from unintended modifications.
- **Real-world modeling:** Models real-world entities using objects, making conceptualization natural.
- **Overcomes limitations of Structured Programming:** Eliminates issues related to global data access and separated data/functions.

**Comparison:**

| Feature | Structured Programming (e.g., C) | Object-Oriented Programming (e.g., Java, C++) |
|---------|-----------------------------------|-----------------------------------------------|
| **Approach** | Top-down approach. | Bottom-up approach. |
| **Focus** | Focuses on functions and process logic. | Focuses on data and objects. |
| **Data Security** | Data moves freely and is less secure. | Data is hidden and secured using encapsulation. |
| **Division** | Program is divided into functions. | Program is divided into objects. |
| **Concepts** | Lacks inheritance and polymorphism. | Supports Inheritance, Polymorphism, Abstraction. |

### 2. Data abstraction and iostream
**Data Abstraction:**
- Abstraction refers to hiding the internal implementation details and showing only the essential features to the user.
- In OOP, it is achieved using Abstract Classes and Interfaces.
- **Example in Java:** A user interacting with a `List` interface only knows about `.add()` and `.remove()` signatures, ignorant of how an `ArrayList` or `LinkedList` implements them internally. 

**iostream (C++ Context):**
- **Note:** `iostream` is a standard library in C++ used for Input/Output operations (Java uses `java.io` and `java.util.Scanner`).
- It stands for Input-Output Stream.
- It contains definitions for objects like `cin` (standard input stream), `cout` (standard output stream), `cerr` (unbuffered error stream), and `clog` (buffered error stream).
- It provides a type-safe object-oriented way of handling I/O operations compared to C's `stdio.h`.

### 3. Storage class specifiers and structure vs class
**Storage Class Specifiers:**
- Specific keywords that define the scope, visibility, and lifetime of variables.
- **In C++:** `auto` (local scope), `register` (hints compiler to store in CPU register), `static` (retains value between function calls, lifetime is entire program), `extern` (global variable, defined elsewhere), `mutable`.
- **In Java:** Java does not use storage classes exactly like C/C++. Instead, it uses **access modifiers** (`public`, `protected`, `private`) and the `static` keyword to determine scope and lifetime.

**Structure vs Class:**

| Feature | Structure (`struct`) | Class (`class`) |
|---------|-----------------------|-----------------|
| **Default Access** | Members are `public` by default (in C++). | Members are `private` by default. |
| **Usage Focus** | Used primarily to group primitive data types. | Used to define complex objects bundling data and logic. |
| **Inheritance** | Does not support inheritance in C, but C++ structs do. | Fully supports inheritance and polymorphism. |
| **Java Context** | Java does **not** have `structs`; it only relies on `classes`. | The fundamental building block of all Java applications. |

### 4. Dynamic constructors and file handling errors
**Dynamic Constructors:**
- A dynamic constructor allocates memory for the object's data members dynamically at runtime (using `new`) during the object creation.
- Helps avoid memory wastage by allocating exactly the required memory length evaluated upon runtime inputs.
- **Example:** In C++, `new` might be used inside constructors for pointer arrays. In Java, objects themselves are always dynamically allocated on the Heap by default when we use `new`.

**File Handling Errors:**
- Errors occurring during file operations like opening, reading, writing, or closing a file.
- **Common File Errors:** File Not Found, Permission Denied, Disk Space Full, Unexpected End of File (EOF).
- **Handling in Java:** Handled using Exceptions (`java.io.IOException`, `FileNotFoundException`). Handled via `try-catch-finally` to ensure file streams and resources are closed safely to prevent memory leaks.

### 5. Exception handling and abstract class vs interface
**Exception Handling:**
- A mechanism to handle runtime errors allowing the normal program execution flow to continue.
- **Keywords:** 
  - `try`: Code that may throw an error.
  - `catch`: Code to handle the exception.
  - `finally`: Block that always executes regardless of an exception (cleanup).
  - `throw`: Explicitly triggers an exception.
  - `throws`: Declares an exception risk in the method signature.

**Abstract Class vs Interface:**

| Feature | Abstract Class | Interface |
|---------|----------------|-----------|
| **Methods** | Can have both abstract and concrete methods. | Implicitly abstract (till Java 8 allowed default/static). |
| **Variables** | Can have final, non-final, static, non-static variables. | Implicitly `public static final`. |
| **Inheritance** | A class can `extend` only one abstract class. | A class can `implement` multiple interfaces. |
| **Constructors**| Can define standard constructors. | Cannot have constructors. |

### 6. Object creation and manipulators
**Object Creation:**
- The process of instantiating a class to hold logic and state in memory. 
- In Java, it happens in three steps:
  1. **Declaration:** `ClassName obj;`
  2. **Instantiation:** `new` operator allocates memory.
  3. **Initialization:** The Constructor is called to initialize fields.
  Example: `Student s1 = new Student();`

**Manipulators (C++ Context):**
- Functions/operators attached directly to output streams to modify format.
- **Examples:** `endl` (newline and flush), `setw(n)` (sets field width), `setprecision(n)` (formatting decimal points).
- **Java Alternative:** Java uses `System.out.printf()` or `String.format()` instead.

### 7. Compile-time vs runtime polymorphism

| Feature | Compile-time Polymorphism (Static Binding) | Runtime Polymorphism (Dynamic Binding) |
|---------|---------------------------------------------|----------------------------------------|
| **Binding Time**| At compile time by compiler. | At runtime by JVM based on actual object type. |
| **Key Mechanism**| Method Overloading (same name, different params).| Method Overriding (same name & params in inheritance). |
| **Speed** | Faster. | Marginally slower due to runtime checks. |
| **Example**| Multiple `add()` functions handling ints, doubles. | Parent `Shape` reference calling `draw()` on Child `Circle`. |

### 8. Constructors and difference from methods
**Constructors:** Special blocks of code used to initialize an object. Invoked automatically when an object is made.

**Difference from Methods:**

| Feature | Constructor | Method |
|---------|-------------|--------|
| **Purpose** | To initialize the state of an object. | To define the behavior of an object. |
| **Name** | Exact same name as the class. | Any valid identifier name. |
| **Return Type** | Does not have a return type (not even `void`). | Must return a type (or `void`). |
| **Invocation** | Triggered implicitly at instantiation. | Triggered explicitly on references. |

### 9. Threads and synchronization
**Threads:**
- A thread is a lightweight sub-process; the smallest unit of CPU processing.
- Multithreading allows simultaneous execution of program segments to maximize CPU usage.
- Created in Java by extending the `Thread` class or implementing the `Runnable` interface.

**Synchronization:**
- Controlling the access of multiple threads to any shared resource to avoid Race Conditions and data corruption.
- In Java, it’s primarily implemented using the `synchronized` keyword applied to methods or blocks. Only the thread holding the monitor lock can enter the synchronized area.

### 10. Generics and VM challenges
**Generics:**
- Introduced in Java 5, it enables parameterizing types. Gives compile-time type safety and removes the need for manual type casting.
- **Example:** `List<String> list = new ArrayList<>();` instead of generic untyped Lists.

**VM (Virtual Machine) Challenges:**
- **Overhead:** Interpreting bytecode and JIT-compiling it incurs performance overhead.
- **Memory Consumption:** Large memory footprint to maintain metadata, the garbage collector, and class schemas.
- **Garbage Collection Pauses:** Intermittent pauses ("stop-the-world") where application threads lock to reclaim memory, hurting real-time capabilities.

### 11. Short notes
- **Java exception:** Unexpected events terminating normal flow. Categorized into Checked (Compile-Time) and Unchecked (Run-Time) exceptions. Handled by try/catch mechanisms.
- **Multithreading:** Concurrent execution paths in one process maximizing CPU multi-core efficiency and responsiveness.
- **Multitasking:** OS capability to execute multiple processes. Process-based vs Thread-based.
- **Garbage collection:** Automatic process reclaiming unreferenced heap memory.
- **Constructor overloading:** Providing multiple constructors with varying parameters allowing an object to be initialized flexibly under multiple scenarios.

---

## Subjective Questions & Solutions (2023)

### 1. JVM and platform independence
- **Platform Independence:** Java is "Write Once, Run Anywhere". The compiler compiles source code into intermediate bytecode (`.class`), which is OS-neutral.
- **Role of JVM:** The Java Virtual Machine executes the bytecode. The JVM itself is platform-dependent (there are distinct JVMs for Windows, Mac, Linux). It dynamically converts the neutral bytecode into instructions the specific host OS CPU can decipher.

### 2. Types of constructors
1. **Default Constructor:** Provided by the Java compiler if no constructors exist. Initializes variables with defaults (0 or null).
2. **No-Argument Constructor:** Manually added to explicitly set default states without requiring parameters.
3. **Parameterized Constructor:** Accepts variable parameters to assign distinct starting values directly.
4. *(Note: Java does not explicitly support Copy Constructors natively like C++; one must manually program a constructor accepting the same Class reference).*

### 3. Abstraction vs encapsulation
| Feature | Abstraction | Encapsulation |
|---------|-------------|---------------|
| **Core Concept** | Hiding implementation complexity and showing only desired features. | Wrapping data layout and methods handling that data into one unit. |
| **Focus area** | Focuses on *what* the object does. | Focuses on *how* the object does it. |
| **Implementation** | Achieved via Abstract classes and Interfaces. | Achieved via access modifiers (`private`, `protected`). |

### 4. Rectangle area program
```java
import java.util.Scanner;

class Rectangle {
    double length, width;

    // Constructor
    Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    double calculateArea() {
        return length * width;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter length: ");
        double l = sc.nextDouble();
        System.out.print("Enter width: ");
        double w = sc.nextDouble();

        Rectangle rect = new Rectangle(l, w);
        System.out.println("Area of Rectangle: " + rect.calculateArea());
    }
}
```

### 5. Inheritance and types
**Inheritance:** Acquiring properties/behaviors of a Superclass. Utilizes `extends` keyword. Enhances reusability.
**Types in Java:**
1. **Single:** Class B extends Class A.
2. **Multilevel:** Class C extends Class B, which extends Class A.
3. **Hierarchical:** Classes B and C both extend Class A.
4. **Multiple:** One class inheriting from multiple superclasses. *Not supported in Java via classes* to prevent the Diamond Problem (ambiguity), but heavily supported through Interfaces.

### 6. Access specifiers
Define the scope and visibility of classes/members.
1. **Private:** Accessible only within the same class context.
2. **Default (No keyword):** Package-private; accessible only within the same package.
3. **Protected:** Accessible within the same package, and outside the package strictly via inheritance (Subclasses).
4. **Public:** Widest scope; accessible fundamentally everywhere.

### 7. Thread model
The life-cycle that memory threads govern:
1. **New:** Instantiated `new Thread()`, ready but not started.
2. **Runnable:** `.start()` invoked. Waiting in a pool for CPU allocation.
3. **Running:** The CPU scheduler dictates runtime and executes `.run()`.
4. **Blocked/Waiting:** Thread is asleep, waiting on an IO operation, or waiting to acquire an object lock.
5. **Terminated / Dead:** Method block completes normally or is interrupted by an uncaught Exception.

### 8. Overloading vs overriding
| Feature | Method Overloading | Method Overriding |
|---------|--------------------|-------------------|
| **Location** | Defined within the same class. | Exists strictly between parent and child (Inheritance). |
| **Signature** | Same method name, **different** parameters. | Exact same name **and** exact same parameters. |
| **Polymorphism** | Compile-Time (Static). | Run-Time (Dynamic). |
| **Modifiers**| Does not strictly limit `static`, `final`, or `private` usage. | Cannot override `private`, `final`, or `static` methods. |

### 9. Layout manager and Swing components
**Layout Managers:** Tools in AWT & Swing formatting and auto-arranging the layouts dynamically to fit windows natively across different OS structures (E.g., `BorderLayout`, `FlowLayout`, `GridLayout`).
**Swing Components:** Lightweight GUI parts in the `javax.swing` package rendering user interactions independent of host environments. Examples: `JFrame` (Container), `JButton` (clickable token), `JTextField` (text input block).

### 10. JDBC and drivers
**JDBC (Java Database Connectivity):** The standard Java API executing direct SQL instructions or updating enterprise DBs dynamically from backend Java programs.
**Drivers:**
1. **Type 1 (JDBC-ODBC bridge):** Obsolete; relies on Windows-specific local ODBC drivers.
2. **Type 2 (Native API):** Maps to Database's Native local libraries written in C.
3. **Type 3 (Network Protocol):** Maps completely through a middleware network proxy server.
4. **Type 4 (Thin Driver):** A Pure Java driver translating JDBC calls natively into the DB server's exclusive network protocol. Usually preferred setup.

### 11. Event handling models
Modern Java (1.1+) uses the **Delegation Event Model** containing three core entities:
1. **Event Source:** UI Element interacting with the user (Button).
2. **Event Object:** Structure capturing what occurred (`ActionEvent`).
3. **Event Listener:** Background entity reacting to the registered Source when clicked (`ActionListener`). It delegates method resolution to blocks like `actionPerformed()`.

### 12. AWT controls
The Abstract Window Toolkit contains heavy-weight GUI assets mapping directly to underlying OS architectures. Main ones include: `Label`, `Button`, `TextField`, `Choice` (Drop-down), `List` (Menu List), `Checkbox`, and grouping `CheckboxGroup` (acts as Radio Buttons).

### 13. Short notes
- **Dynamic dispatch:** The JVM dynamically binds overridden logic methods at exact execution runtime according to the Object type initialized at `new`, rather than the reference pointer class variable type.
- **Iterator:** Universal collection loop traversal instance handling stepping `hasNext()` and returning `next()`.
- **Synchronization:** Halting access blocks locking threads securely enabling data continuity avoiding corruption.
- **TCP/IP socket:** Stream-based networking protocol standardizing `Socket` client pipes securely talking to `ServerSocket` streams bi-directionally.

---

## Subjective Questions & Solutions (2022)

### 1. Data types and type casting
**Data Types:** Define variable schemas. Two tiers in Java: 
1. Primitive (value-stored): `int`, `boolean`, `char`, `double`.
2. Reference: Objects, Classes, Arrays.

**Type Casting:** Modifying variable scales.
1. **Implicit (Widening):** Auto-handled upscaling a smaller primitive to larger without destruction (`int` → `long`).
2. **Explicit (Narrowing):** Forced downsizing via manual notation code causing truncations (`double` → `int` via `(int)` tag).

### 2. OOP principles
1. **Encapsulation:** Wrapping attributes and functions firmly preventing chaotic states.
2. **Abstraction:** Displaying minimalist functionality while shielding heavy background code layouts.
3. **Inheritance:** Enabling hierarchical object schemas inheriting code from higher roots reducing redundancies.
4. **Polymorphism:** Having one naming semantic perform entirely differing things (Static + Dynamic resolutions).

### 3. Class vs object
| Feature | Class | Object |
|---------|-------|--------|
| **Definition** | The theoretical blueprint structure. | The active realized entity. |
| **Logic Space** | Logical framework (Uses NO active memory footprint until invoked). | Exists on the live Heap occupying true memory. |
| **Declaration phase**| Established once via `class`.| Created infinitely utilizing the `new` logic. |

### 4. Circle program
```java
import java.util.Scanner;

class Circle {
    double radius;
    final double PI = 3.14159;

    Circle(double radius) {
        this.radius = radius;
    }

    double getArea() {
        return PI * radius * radius;
    }

    double getCircumference() {
        return 2 * PI * radius;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter radius: ");
        double r = sc.nextDouble();

        Circle c = new Circle(r);
        System.out.println("Area: " + c.getArea());
        System.out.println("Circumference: " + c.getCircumference());
    }
}
```

### 5. Exception handling steps
When a runtime anomaly is caught:
1. Exogenous fault disrupts `try` logic. An Error Object spawns.
2. The Engine searches for hierarchical `catch` routines mapping correctly to that exact spawned class type.
3. The mapped `catch` scope activates rendering graceful error printouts or system resets.
4. The compulsory `finally` logic clears all dangling operations (Connections closed, Buffers flushed).
5. Sequential baseline execution resumes securely below the block.

### 6. Try-catch multiple exceptions
One isolated `try` target block cascaded by multiple specialized `catch` targets providing granular resolutions.
- Crucial aspect: Derived exception classes (e.g. `ArithmeticException`) strictly MUST be placed above generalized root exceptions (`Exception`), otherwise the code refuses compilation indicating 'Unreachable Code block'.

### 7. Packages and advantages
**Packages:** A directory structure containing similar categorized classes helping developers.
**Advantages:**
- Completely prevents namespace collisions (You can have dual `Node` modules contained across differing folders).
- Enforces Access rules seamlessly keeping variables inside packages locked away from outer access scopes.
- Easier locating and code administration.

### 8. super keyword
Tethers children tightly to direct parent superclass assets. Used for:
1. Recovering a hidden parent variable obscured by identical child instance variable string names (`super.val`).
2. Invoking overrode parent methods forcibly (`super.printData()`).
3. Routing parent-specific initialization structures forcefully via `super()` executing parent setup constructors inside children architectures.

### 9. Applet lifecycle
(Deprecated web-level Java)
1. `init()`: Starts baseline parameters.
2. `start()`: Execution payload activated dynamically.
3. `paint(Graphics)`: Draw triggers deploying visual models contextually.
4. `stop()`: Called dynamically whenever user window interaction toggles away securely halting resource bleeding.
5. `destroy()`: Purged violently out of RAM space completely unallocated. 

### 10. JDBC role
- Operates primarily bridging pure Java OOP frameworks into pure Relational SQL spaces safely.
- Grants dynamic statement compilations generating live Prepared Statements mitigating Injection flaws.
- Interrogates Database queries delivering normalized scalable Result Sets to frontend users safely bypassing backend configurations.

### 11. Layout managers
Manages standard dimensional formatting guaranteeing UI models don't skew across macOS, Windows, or Linux visual constraints preventing absolute alignment overlaps. Examples include Standard Flows (`FlowLayout`), and grid schemas (`GridLayout`).

### 12. AWT vs Swing
- **AWT (Abstract Window Toolkit):** Heavyweight. Ties visual rendering tightly to OS-bound native modules rendering speediest loads but creating visual discrepancies between Macs and PCs.
- **Swing:** Lightweight. Operates completely bypassing OS graphics modules generating pure Java pixel drawings identically on every single screen at the cost of slight execution delay. Built via powerful MVC pattern standardizations.

### 13. Short notes
- **Wrapper class:** Allows placing native un-typed primitive formats into strictly OOP frameworks (`List<Integer>`) securely via Boxing/Unboxing phases.
- **Garbage collection:** Identifies orphaned dangling pointer logic, wiping unused array data returning Heap memory blocks cleanly avoiding manual `free()` tracking routines.
- **RMI (Remote Method Invocation):** Remote execution sockets deploying methods inside isolated Java Engines spanning across entirely split internet domains seamlessly orchestrating distributed code clouds.
- **Thread priorities:** JVM scheduling queues dictating which processor threads take absolute logic priority. (Scale 1 to 10; 1 = minimal priority, 10 = absolute critical OS priority).
