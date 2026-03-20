# UNIT 3: Packages, Interfaces & Exception Handling

---

## PART A: PACKAGES

---

## 1. Packages in Java

### 1.1 Definition

A **package** is a mechanism for **organizing related classes and interfaces** into a single namespace. It is like a **folder** in a file system.

### 1.2 Types of Packages

```
              Packages
         ┌────────┴─────────┐
    Built-in           User-defined
    Packages           Packages
         │
    ┌────┼────┬────┬────┐
    │    │    │    │    │
java.  java. java. java. java.
lang   util  io   net   awt
```

### 1.3 Built-in Packages (Exam Important ⭐)

| Package | Description | Key Classes |
|---------|-------------|-------------|
| `java.lang` | Core classes (auto-imported) | String, Math, Object, System, Thread, Integer |
| `java.util` | Utility classes | ArrayList, HashMap, Scanner, Date, Collections |
| `java.io` | Input/Output | File, InputStream, OutputStream, BufferedReader |
| `java.net` | Networking | Socket, URL, ServerSocket, InetAddress |
| `java.awt` | GUI (Abstract Window Toolkit) | Frame, Button, Label, TextField |
| `javax.swing` | Advanced GUI | JFrame, JButton, JLabel, JPanel |
| `java.sql` | Database | Connection, Statement, ResultSet, DriverManager |
| `java.math` | Math operations | BigInteger, BigDecimal |

### 1.4 Creating a User-Defined Package

```java
// File: mypackage/Calculator.java
package mypackage;  // MUST be the FIRST statement

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int subtract(int a, int b) {
        return a - b;
    }
    
    public int multiply(int a, int b) {
        return a * b;
    }
    
    public double divide(int a, int b) {
        if (b == 0) throw new ArithmeticException("Division by zero");
        return (double) a / b;
    }
}
```

### 1.5 Package Directory Structure

```
ProjectRoot/
├── mypackage/
│   ├── Calculator.java
│   └── MathHelper.java
├── mypackage/subpackage/
│   └── AdvancedMath.java
└── Main.java
```

### 1.6 Rules for Packages

1. `package` statement must be the **first line** (before import)
2. Only **one package statement** per file
3. Package name should be in **lowercase**
4. Convention: reverse domain name (`com.company.project`)
5. Package creates a corresponding **directory structure**

### 1.7 Compiling and Running with Packages

```bash
# Compile
javac -d . Calculator.java
# This creates: ./mypackage/Calculator.class

# Run
java mypackage.Calculator
```

---

## 2. Access Protection in Packages

### 2.1 Access Modifier Table (Exam Important ⭐)

| Access Level | Same Class | Same Package | Subclass (Diff Package) | Different Package |
|:--|:--:|:--:|:--:|:--:|
| `public` | ✓ | ✓ | ✓ | ✓ |
| `protected` | ✓ | ✓ | ✓ | ✗ |
| `default` (no modifier) | ✓ | ✓ | ✗ | ✗ |
| `private` | ✓ | ✗ | ✗ | ✗ |

### 2.2 Example

```java
// File: package1/A.java
package package1;

public class A {
    public int pubVar = 1;        // Accessible everywhere
    protected int proVar = 2;     // Same pkg + subclass
    int defVar = 3;               // Same package only (default)
    private int priVar = 4;       // This class only
    
    public void showAll() {
        System.out.println(pubVar + " " + proVar + " " + defVar + " " + priVar);
        // All accessible within same class ✓
    }
}

// File: package1/B.java (Same Package)
package package1;

class B {
    void test() {
        A obj = new A();
        System.out.println(obj.pubVar);   // ✓ public
        System.out.println(obj.proVar);   // ✓ protected (same package)
        System.out.println(obj.defVar);   // ✓ default (same package)
        // System.out.println(obj.priVar); // ✗ private
    }
}

// File: package2/C.java (Different Package, Subclass)
package package2;
import package1.A;

class C extends A {
    void test() {
        System.out.println(pubVar);       // ✓ public
        System.out.println(proVar);       // ✓ protected (subclass)
        // System.out.println(defVar);     // ✗ default (diff package)
        // System.out.println(priVar);     // ✗ private
    }
}

// File: package2/D.java (Different Package, NOT subclass)
package package2;
import package1.A;

class D {
    void test() {
        A obj = new A();
        System.out.println(obj.pubVar);   // ✓ public
        // System.out.println(obj.proVar); // ✗ protected (not subclass)
        // System.out.println(obj.defVar); // ✗ default (diff package)
        // System.out.println(obj.priVar); // ✗ private
    }
}
```

---

## 3. Importing Packages

### 3.1 Ways to Import

```java
// 1. Import a specific class
import java.util.ArrayList;

// 2. Import all classes from a package
import java.util.*;

// 3. Fully qualified name (no import needed)
java.util.ArrayList<String> list = new java.util.ArrayList<>();

// 4. Static import (import static members)
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;
```

### 3.2 Import Rules

| Rule | Description |
|------|-------------|
| `java.lang.*` is auto-imported | No need to import String, System, Math, etc. |
| Import specific class is preferred | `import java.util.ArrayList` is better than `import java.util.*` |
| Sub-packages NOT auto-imported | `import java.util.*` does NOT import `java.util.concurrent.*` |
| Only `public` classes can be imported | Non-public classes are package-private |
| Import statement comes after `package` | `package` → `import` → `class` |

### 3.3 Static Import
```java
import static java.lang.Math.*;

public class StaticImportDemo {
    public static void main(String[] args) {
        // Without static import: Math.sqrt(25), Math.PI
        // With static import:
        double result = sqrt(25);     // Direct use
        double area = PI * 5 * 5;    // Direct use
        System.out.println("Result: " + result);
        System.out.println("Area: " + area);
    }
}
```

---

## PART B: INTERFACES

---

## 4. Interface in Java

### 4.1 Definition

An **interface** is a **fully abstract type** that specifies **what a class must do**, but not **how** it does it. It defines a **contract** that implementing classes must follow.

### 4.2 Syntax

```java
interface InterfaceName {
    // Constants (public static final by default)
    int MAX_VALUE = 100;
    
    // Abstract methods (public abstract by default)
    void method1();
    int method2(int x);
    
    // Default method (Java 8+)
    default void method3() {
        System.out.println("Default implementation");
    }
    
    // Static method (Java 8+)
    static void method4() {
        System.out.println("Static method in interface");
    }
}
```

### 4.3 Key Properties

| Property | Description |
|----------|-------------|
| All methods are `public abstract` by default | (Before Java 8) |
| `default` and `static` methods allowed | (Java 8+) |
| All variables are `public static final` | Constants only |
| Cannot have constructors | No instantiation |
| Cannot have instance variables | Only constants |
| A class can implement multiple interfaces | Multiple inheritance support |
| An interface can extend other interfaces | Using `extends` |

### 4.4 Complete Example

```java
// Interface 1
interface Drawable {
    void draw();
}

// Interface 2
interface Resizable {
    void resize(double factor);
    
    default void resetSize() {
        System.out.println("Resetting to default size");
    }
}

// Class implementing multiple interfaces
class Circle implements Drawable, Resizable {
    double radius;
    
    Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing circle with radius: " + radius);
    }
    
    @Override
    public void resize(double factor) {
        radius *= factor;
        System.out.println("Resized to radius: " + radius);
    }
}

public class InterfaceDemo {
    public static void main(String[] args) {
        Circle c = new Circle(5);
        c.draw();           // Drawing circle with radius: 5
        c.resize(2);        // Resized to radius: 10
        c.resetSize();      // Resetting to default size (default method)
        
        // Interface reference
        Drawable d = new Circle(3);
        d.draw();           // ✓
        // d.resize(2);     // ✗ Drawable doesn't have resize()
    }
}
```

---

## 5. Implementing Interfaces

### 5.1 Rules

1. A class uses `implements` keyword
2. Must provide implementation for **ALL abstract methods**
3. Methods must be declared `public` (since interface methods are public)
4. A class can implement **multiple interfaces**
5. An abstract class can implement an interface **without implementing all methods**

### 5.2 Multiple Interface Implementation

```java
interface Flying {
    void fly();
}

interface Swimming {
    void swim();
}

interface Running {
    void run();
}

// Implementing multiple interfaces
class Duck implements Flying, Swimming, Running {
    @Override
    public void fly() { System.out.println("Duck is flying"); }
    
    @Override
    public void swim() { System.out.println("Duck is swimming"); }
    
    @Override
    public void run() { System.out.println("Duck is running"); }
}

// Partial implementation using abstract class
abstract class Bird implements Flying {
    String name;
    // Not implementing fly() — subclass must do it
}
```

---

## 6. Variables in Interfaces

### 6.1 Key Points

All variables in an interface are implicitly **`public static final`** (constants).

```java
interface Constants {
    // All of these are the same:
    int MAX = 100;                           // implicitly public static final
    public static final int MIN = 0;         // explicitly declared
    
    double PI = 3.14159;
    String APP_NAME = "MyApp";
}

class MyClass implements Constants {
    void show() {
        System.out.println(MAX);         // 100
        System.out.println(MIN);         // 0
        System.out.println(PI);          // 3.14159
        System.out.println(APP_NAME);    // MyApp
        
        // MAX = 200;  // ERROR: Cannot assign value to final variable
    }
}

// Can also access without implementing
class Other {
    void test() {
        System.out.println(Constants.MAX);  // Using interface name
    }
}
```

---

## 7. Interfaces Can Be Extended

Interfaces can extend **one or more** other interfaces using `extends`.

```java
interface A {
    void methodA();
}

interface B {
    void methodB();
}

// Interface extending multiple interfaces
interface C extends A, B {
    void methodC();
}

// Class implementing C must implement ALL methods (A + B + C)
class MyClass implements C {
    @Override
    public void methodA() { System.out.println("Method A"); }
    
    @Override
    public void methodB() { System.out.println("Method B"); }
    
    @Override
    public void methodC() { System.out.println("Method C"); }
}
```

```
Interface Inheritance:
┌─────────┐   ┌─────────┐
│   A     │   │    B    │
│methodA()│   │methodB()│
└────┬────┘   └────┬────┘
     └──────┬──────┘
        ┌───────┐
        │   C   │  extends A, B
        │methodC│
        └───┬───┘
        ┌───────┐
        │MyClass│  implements C
        │(all 3 │
        │methods)│
        └───────┘
```

---

## PART C: EXCEPTION HANDLING

---

## 8. Exception Handling in Java

### 8.1 What is an Exception?

An **exception** is an **abnormal event** that occurs during program execution and disrupts the normal flow.

### 8.2 Exception Hierarchy (Exam Important ⭐)

```
                    ┌───────────┐
                    │ Throwable │
                    └─────┬─────┘
              ┌───────────┴───────────┐
              ↓                       ↓
        ┌───────────┐          ┌───────────┐
        │   Error   │          │ Exception │
        └─────┬─────┘          └─────┬─────┘
              │                ┌─────┴──────────┐
              │                ↓                 ↓
        StackOverflow    ┌───────────────┐ ┌──────────────────┐
        OutOfMemory      │RuntimeException│ │ Checked Exceptions│
        VirtualMachine   │ (Unchecked)    │ │ IOException       │
        Error            │               │ │ SQLException      │
                         │NullPointer     │ │ FileNotFound      │
                         │ArrayIndexOOB   │ │ ClassNotFound     │
                         │ArithmeticExc   │ └──────────────────┘
                         │ClassCast       │
                         │NumberFormat    │
                         └───────────────┘
```

### 8.3 Checked vs Unchecked Exceptions (Exam Important ⭐)

| Feature | Checked Exception | Unchecked Exception |
|---------|-------------------|---------------------|
| **Checked at** | Compile-time | Runtime |
| **Must handle** | Yes (try-catch or throws) | No (optional) |
| **Extends** | `Exception` (not RuntimeException) | `RuntimeException` |
| **Examples** | IOException, SQLException, FileNotFoundException | NullPointerException, ArrayIndexOutOfBoundsException, ArithmeticException |
| **Cause** | External factors (file not found, network error) | Programming bugs (null access, wrong index) |
| **Recovery** | Usually recoverable | Usually indicates bugs |

---

## 9. Using Try & Catch

### 9.1 Syntax

```java
try {
    // Code that might throw an exception
    // (risky code)
} catch (ExceptionType e) {
    // Code to handle the exception
    // (recovery code)
}
```

### 9.2 Example

```java
public class TryCatchDemo {
    public static void main(String[] args) {
        try {
            int a = 10, b = 0;
            int result = a / b;  // ArithmeticException!
            System.out.println("Result: " + result);  // NOT executed
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero!");
            System.out.println("Exception: " + e.getMessage());
        }
        
        System.out.println("Program continues normally");
    }
}
/* Output:
   Error: Cannot divide by zero!
   Exception: / by zero
   Program continues normally
*/
```

### 9.3 Flow of Try-Catch

```
try {
    Statement 1  ──→ executes
    Statement 2  ──→ EXCEPTION occurs!
    Statement 3  ──→ SKIPPED (not executed)
}                    │
catch (Exception e) {│
    Handler code ←───┘  (catches the exception)
}
Next statement ──→ executes normally
```

---

## 10. Multiple Catch Blocks

### 10.1 Syntax

```java
try {
    // risky code
} catch (ArithmeticException e) {
    // handle arithmetic error
} catch (ArrayIndexOutOfBoundsException e) {
    // handle array index error
} catch (NullPointerException e) {
    // handle null pointer error
} catch (Exception e) {
    // catch-all for any other exception
    // MUST be the LAST catch block
}
```

### 10.2 Complete Example

```java
public class MultipleCatchDemo {
    public static void main(String[] args) {
        try {
            int[] arr = {1, 2, 3};
            
            // Uncomment one to test different exceptions:
            // int result = 10 / 0;                    // ArithmeticException
            // int x = arr[5];                          // ArrayIndexOutOfBoundsException
            // String s = null; s.length();             // NullPointerException
            
            System.out.println("No exception occurred");
            
        } catch (ArithmeticException e) {
            System.out.println("Arithmetic Error: " + e.getMessage());
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array Index Error: " + e.getMessage());
        } catch (NullPointerException e) {
            System.out.println("Null Pointer Error: " + e.getMessage());
        } catch (Exception e) {
            System.out.println("General Error: " + e.getMessage());
        }
    }
}
```

### 10.3 Multi-Catch (Java 7+)

```java
try {
    // risky code
} catch (ArithmeticException | ArrayIndexOutOfBoundsException e) {
    // Handle both exceptions with single catch block
    System.out.println("Error: " + e.getMessage());
}
```

### 10.4 Important Rules for Multiple Catch

1. **More specific exceptions FIRST** — subclass before superclass
2. **`Exception` must be LAST** — it's the parent of all exceptions
3. **Only one catch block executes** — first matching one
4. **Unreachable catch** causes compile error (parent before child)

```java
// WRONG ORDER - Compile Error!
catch (Exception e) { }           // Parent first — catches everything
catch (ArithmeticException e) { } // Unreachable!

// CORRECT ORDER
catch (ArithmeticException e) { } // Specific first
catch (Exception e) { }           // General last
```

---

## 11. Throw, Throws, and Finally

### 11.1 The `throw` Keyword

Used to **explicitly throw an exception** from a method or block.

```java
public class ThrowDemo {
    static void validateAge(int age) {
        if (age < 18) {
            throw new ArithmeticException("Not eligible to vote");
                   // ↑ Creating and throwing exception explicitly
        }
        System.out.println("Welcome to vote!");
    }
    
    public static void main(String[] args) {
        try {
            validateAge(15);  // Will throw exception
        } catch (ArithmeticException e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
```

### 11.2 The `throws` Keyword

Used in **method declaration** to indicate that the method **might throw** specified exceptions. Delegates exception handling to the **caller**.

```java
import java.io.*;

public class ThrowsDemo {
    // Method declares that it might throw IOException
    static void readFile(String filename) throws IOException {
        FileReader fr = new FileReader(filename);
        BufferedReader br = new BufferedReader(fr);
        System.out.println(br.readLine());
        br.close();
    }
    
    public static void main(String[] args) {
        try {
            readFile("test.txt");
        } catch (IOException e) {
            System.out.println("File error: " + e.getMessage());
        }
    }
}
```

### 11.3 throw vs throws

| Feature | `throw` | `throws` |
|---------|---------|----------|
| **Purpose** | Actually throws an exception | Declares possible exceptions |
| **Where** | Inside method body | In method signature |
| **Syntax** | `throw new Exception()` | `void method() throws Exception` |
| **Count** | Throws ONE exception at a time | Can declare MULTIPLE exceptions |
| **Type** | Followed by exception object | Followed by exception class names |
| **What follows** | Instance of Throwable | Class names (comma separated) |

### 11.4 The `finally` Block

The `finally` block **always executes** regardless of whether an exception occurs or not. Used for **cleanup operations** (closing files, connections, etc.).

```java
public class FinallyDemo {
    public static void main(String[] args) {
        FileReader fr = null;
        try {
            fr = new FileReader("test.txt");
            // Read file operations
            System.out.println("File opened successfully");
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        } finally {
            // ALWAYS executes - cleanup code
            System.out.println("Finally block executed");
            try {
                if (fr != null) fr.close();
            } catch (IOException e) {
                System.out.println("Error closing file");
            }
        }
    }
}
```

### 11.5 Finally Block — When Does It Execute?

```
Case 1: No exception
try { ... }     ──→ executes
catch { }       ──→ SKIPPED
finally { }     ──→ executes ✓

Case 2: Exception caught
try { ... }     ──→ exception occurs!
catch { ... }   ──→ handles exception
finally { }     ──→ executes ✓

Case 3: Exception NOT caught
try { ... }     ──→ exception occurs!
catch { ... }   ──→ wrong type, not caught
finally { }     ──→ executes ✓ (then exception propagates)

Case 4: Return in try
try { return; } ──→ wants to return
finally { }     ──→ executes ✓ BEFORE return

Only NOT executed: System.exit() or JVM crash
```

### 11.6 Try-with-Resources (Java 7+)

```java
// Automatically closes resources
try (FileReader fr = new FileReader("test.txt");
     BufferedReader br = new BufferedReader(fr)) {
    
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    System.out.println("Error: " + e.getMessage());
}
// fr and br are automatically closed — no need for finally!
```

---

## 12. Java's Built-in Exceptions

### 12.1 Common Unchecked Exceptions (RuntimeException)

| Exception | Cause | Example |
|-----------|-------|---------|
| `ArithmeticException` | Division by zero | `int x = 10/0;` |
| `NullPointerException` | Accessing null reference | `String s = null; s.length();` |
| `ArrayIndexOutOfBoundsException` | Invalid array index | `int[] a = {1,2}; a[5];` |
| `StringIndexOutOfBoundsException` | Invalid string index | `"abc".charAt(5);` |
| `NumberFormatException` | Invalid number conversion | `Integer.parseInt("abc");` |
| `ClassCastException` | Invalid type casting | `Object o = "hello"; Integer i = (Integer)o;` |
| `IllegalArgumentException` | Invalid method argument | Passing negative value where positive required |
| `StackOverflowError` | Infinite recursion | Method calling itself infinitely |
| `NegativeArraySizeException` | Creating array with negative size | `new int[-5];` |

### 12.2 Common Checked Exceptions

| Exception | Cause |
|-----------|-------|
| `IOException` | I/O operation failure |
| `FileNotFoundException` | File doesn't exist |
| `SQLException` | Database access error |
| `ClassNotFoundException` | Class not found during loading |
| `InterruptedException` | Thread interrupted |
| `CloneNotSupportedException` | Object cloning not supported |

---

## 13. User-Defined (Custom) Exceptions (Exam Important ⭐)

### 13.1 Creating Custom Exceptions

```java
// Custom Checked Exception
class InsufficientBalanceException extends Exception {
    private double amount;
    
    InsufficientBalanceException(double amount) {
        super("Insufficient balance! Tried to withdraw: " + amount);
        this.amount = amount;
    }
    
    public double getAmount() {
        return amount;
    }
}

// Custom Unchecked Exception
class InvalidAgeException extends RuntimeException {
    InvalidAgeException(String message) {
        super(message);
    }
}
```

### 13.2 Complete Example

```java
// Custom Exception
class InsufficientBalanceException extends Exception {
    double amount;
    
    InsufficientBalanceException(double amount) {
        super("Cannot withdraw Rs." + amount + " — Insufficient balance!");
        this.amount = amount;
    }
}

// Bank Account class using custom exception
class BankAccount {
    private double balance;
    private String accountHolder;
    
    BankAccount(String name, double balance) {
        this.accountHolder = name;
        this.balance = balance;
    }
    
    void deposit(double amount) {
        if (amount <= 0)
            throw new IllegalArgumentException("Deposit amount must be positive");
        balance += amount;
        System.out.println("Deposited: Rs." + amount);
    }
    
    void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException(amount);
        }
        balance -= amount;
        System.out.println("Withdrawn: Rs." + amount);
    }
    
    double getBalance() {
        return balance;
    }
}

public class CustomExceptionDemo {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount("Rahul", 5000);
        
        try {
            acc.deposit(2000);
            System.out.println("Balance: Rs." + acc.getBalance());
            
            acc.withdraw(3000);
            System.out.println("Balance: Rs." + acc.getBalance());
            
            acc.withdraw(10000);  // This will throw exception
            
        } catch (InsufficientBalanceException e) {
            System.out.println("Exception: " + e.getMessage());
            System.out.println("Attempted amount: Rs." + e.amount);
        }
    }
}
/* Output:
   Deposited: Rs.2000.0
   Balance: Rs.7000.0
   Withdrawn: Rs.3000.0
   Balance: Rs.4000.0
   Exception: Cannot withdraw Rs.10000.0 — Insufficient balance!
   Attempted amount: Rs.10000.0
*/
```

### 13.3 Steps to Create Custom Exception

```
Step 1: Create a class extending Exception (checked)
        or RuntimeException (unchecked)
           ↓
Step 2: Add constructors (usually with String message)
           ↓
Step 3: Optionally add custom fields and methods
           ↓
Step 4: Throw using 'throw new YourException()'
           ↓
Step 5: Handle using try-catch or declare with 'throws'
```

---

## 14. Nested Try Blocks

```java
public class NestedTryDemo {
    public static void main(String[] args) {
        try {  // Outer try
            System.out.println("Outer try block");
            
            try {  // Inner try
                int[] arr = new int[5];
                arr[10] = 50;  // ArrayIndexOutOfBounds
            } catch (ArrayIndexOutOfBoundsException e) {
                System.out.println("Inner catch: " + e.getMessage());
            }
            
            int result = 10 / 0;  // ArithmeticException
            
        } catch (ArithmeticException e) {
            System.out.println("Outer catch: " + e.getMessage());
        } finally {
            System.out.println("Finally block");
        }
    }
}
/* Output:
   Outer try block
   Inner catch: Index 10 out of bounds for length 5
   Outer catch: / by zero
   Finally block
*/
```

---

## 15. Exception Propagation

```
Method Stack:
main() → method1() → method2() → method3()

If method3() throws exception:
method3() → can it handle? NO → propagates to method2()
method2() → can it handle? NO → propagates to method1()
method1() → can it handle? YES → CAUGHT here

If NO method handles it → JVM default handler → Program terminates
```

```java
class PropagationDemo {
    static void method3() {
        int result = 10 / 0;  // Exception occurs here
    }
    
    static void method2() {
        method3();  // Exception propagates up
    }
    
    static void method1() {
        try {
            method2();  // Exception caught here
        } catch (ArithmeticException e) {
            System.out.println("Exception caught in method1: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        method1();
    }
}
// Output: Exception caught in method1: / by zero
```

---

## 16. Important Exam Questions

### Short Answer Questions
1. What is a package? List any 5 built-in Java packages.
2. Differentiate between checked and unchecked exceptions.
3. What is the difference between `throw` and `throws`?
4. What is `finally`? When does it NOT execute?
5. Differentiate between abstract class and interface.
6. What are access modifiers? Draw the access level table.
7. Can an interface have variables? Explain.

### Long Answer Questions
1. Explain packages in Java. How to create, compile, and use user-defined packages?
2. What are interfaces? Explain with example how Java achieves multiple inheritance using interfaces.
3. Explain exception handling in Java with try, catch, throw, throws, and finally with examples.
4. Write a Java program demonstrating user-defined exceptions.
5. Explain the exception hierarchy in Java with a diagram.
6. Write a program that demonstrates multiple catch blocks and nested try blocks.
7. Explain access protection in Java with a table showing visibility across packages.

---

> **Exam Tip:** For exception handling questions, always draw the **Exception Hierarchy diagram** and explain the difference between `Error`, `Checked Exception`, and `Unchecked Exception`.
