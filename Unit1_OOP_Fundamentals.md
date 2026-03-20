# UNIT 1: Object-Oriented Programming Fundamentals

---

## 1. Object-Oriented Thinking — A Way of Viewing the World

### 1.1 What is Object-Oriented Thinking?

Object-Oriented Thinking is a way of **modeling the real world** by viewing everything as **objects** that interact with each other. Instead of thinking in terms of procedures or functions, we think in terms of **entities (objects)** that have:

- **State** (attributes/data)
- **Behavior** (methods/functions)
- **Identity** (unique existence)

### 1.2 Real-World Analogy

| Real World | OOP Concept |
|------------|-------------|
| Car | Object |
| Blueprint of a Car | Class |
| Color, Speed, Model | Attributes (State) |
| Start(), Stop(), Accelerate() | Methods (Behavior) |
| Registration Number | Identity |

### 1.3 Key Principles of OO Thinking

1. **Everything is an Object** — Every entity in the problem domain is modeled as an object
2. **Objects communicate by sending messages** — Objects interact through method calls
3. **Each object has its own memory** — Objects store their own data (attributes)
4. **Every object is an instance of a class** — Classes are templates for objects
5. **A class groups similar objects** — All objects of a class share the same structure

### 1.4 Viewing the World through OOP

```
Real World Problem
       ↓
Identify Objects (Nouns)
       ↓
Identify Attributes (Adjectives/Properties)
       ↓
Identify Behaviors (Verbs/Actions)
       ↓
Identify Relationships (is-a, has-a)
       ↓
Design Classes and Interactions
       ↓
Implement in Code
```

**Example:** A Bank System
- **Objects:** Customer, Account, Transaction, Bank
- **Attributes:** Customer(name, address), Account(balance, accountNo)
- **Behaviors:** Account.deposit(), Account.withdraw(), Transaction.process()
- **Relationships:** Customer HAS-A Account, SavingsAccount IS-A Account

---

## 2. Computation as Simulation

### 2.1 Concept

In OOP, **computation is viewed as a simulation of the real world**. The program creates a "virtual world" where objects exist, interact, and collaborate to solve problems—just like in the real world.

### 2.2 Key Ideas

| Traditional Programming | OOP (Simulation) |
|------------------------|-------------------|
| Program = Algorithms + Data Structures | Program = Collection of interacting objects |
| Focus on procedures | Focus on objects and their interactions |
| Data and functions are separate | Data and functions are encapsulated together |
| Top-down decomposition | Bottom-up design |

### 2.3 How Simulation Works

```
┌──────────────────────────────────────────────────┐
│              SIMULATION MODEL                     │
│                                                   │
│   ┌──────────┐  message   ┌──────────┐           │
│   │ Object A │ --------→  │ Object B │           │
│   │ (Student) │            │ (Library)│           │
│   └──────────┘            └──────────┘           │
│        ↑                       │                  │
│        │      message          │                  │
│        │    ┌──────────┐       ↓                  │
│        └────│ Object C │ ←─────┘                  │
│             │ (Book)   │                          │
│             └──────────┘                          │
└──────────────────────────────────────────────────┘
```

**Example:** ATM Machine Simulation
- Objects: ATM, Card, Account, Bank, Screen, Keypad
- The program simulates real ATM operations through object interactions

---

## 3. Messages and Methods

### 3.1 Messages

A **message** is a request sent from one object to another to perform some action. It consists of:

1. **Receiver** — The object to which the message is sent
2. **Method name** — The name of the action to perform
3. **Arguments** — Additional information needed

```java
// Message: asking account object to deposit 5000
account.deposit(5000);
//  ↑         ↑       ↑
// receiver  method  argument
```

### 3.2 Methods

A **method** is a function defined inside a class that describes the **behavior** of the object. When a message is received, the corresponding method is executed.

```java
class Account {
    double balance;
    
    // Method that responds to "deposit" message
    void deposit(double amount) {
        balance += amount;
        System.out.println("Deposited: " + amount);
    }
    
    // Method that responds to "withdraw" message
    void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
        } else {
            System.out.println("Insufficient balance");
        }
    }
}
```

### 3.3 Message Passing Mechanism

```
┌────────────┐    deposit(5000)    ┌────────────┐
│  Sender    │ ─────────────────→  │  Receiver  │
│  (main)    │                     │  (account) │
│            │  ←─────────────────  │            │
│            │    "Deposited"       │  execute   │
│            │                     │  deposit() │
└────────────┘                     └────────────┘
```

### 3.4 Importance of Message Passing (Exam Important)

| Feature | Description |
|---------|-------------|
| Decoupling | Sender doesn't need to know internal implementation |
| Encapsulation | Internal details are hidden from the sender |
| Flexibility | Receiver can change implementation without affecting sender |
| Polymorphism | Different objects can respond to the same message differently |

---

## 4. A Brief History of Object-Oriented Programming

### 4.1 Evolution Timeline

```
1960s ──→ 1970s ──→ 1980s ──→ 1990s ──→ 2000s
  │         │         │         │         │
Simula   Smalltalk   C++    Java/     C#/
(1967)   (1972)    (1979)  Python   Kotlin
  │         │         │     (1995)     │
First    Pure OOP  OOP+C    Web Era  Modern
OOP                                   OOP
```

### 4.2 Key Milestones

| Year | Language | Contribution |
|------|----------|-------------|
| **1967** | **Simula** | First OOP language; introduced classes and objects (Ole-Johan Dahl & Kristen Nygaard) |
| **1972** | **Smalltalk** | First pure OOP language; everything is an object (Alan Kay, Xerox PARC) |
| **1979** | **C++** | Combined C with OOP features (Bjarne Stroustrup) |
| **1984** | **Objective-C** | Used in Apple/Mac development |
| **1995** | **Java** | Platform-independent, secure, robust OOP (James Gosling, Sun Microsystems) |
| **2000** | **C#** | Microsoft's OOP language for .NET framework |
| **2011** | **Kotlin** | Modern OOP language for JVM |

### 4.3 Alan Kay's Definition of OOP

Alan Kay (inventor of Smalltalk) defined OOP based on:
1. **Everything is an object**
2. **Objects communicate by sending and receiving messages**
3. **Objects have their own memory (state)**
4. **Every object is an instance of a class**
5. **The class holds the shared behavior for its instances**
6. **To evaluate a message, control is given to the receiver**

---

## 5. The History of Java

### 5.1 Origin of Java

| Aspect | Detail |
|--------|--------|
| **Creator** | James Gosling |
| **Company** | Sun Microsystems (later acquired by Oracle in 2010) |
| **Year** | 1991 (started as "Oak"), renamed to Java in 1995 |
| **Original Purpose** | Consumer electronic devices (set-top boxes, TVs) |
| **Release** | Java 1.0 released in January 1996 |

### 5.2 Why was Java Created?

1. **Platform Independence** — Need for code that runs on different processors
2. **Embedded Systems** — Code for consumer electronics needed reliability
3. **Internet/Web** — With the rise of the web, Java found its true calling (Applets)
4. **Security** — Needed a secure language for distributed environments

### 5.3 Timeline of Java

```
1991: "Green Project" started at Sun Microsystems
       │
1992: "Oak" language created by James Gosling
       │  (named after an oak tree outside his office)
       │
1995: Renamed to "Java" (after Java coffee)
       │  Presented at SunWorld conference
       │
1996: Java 1.0 released — "Write Once, Run Anywhere"
       │
1998: Java 2 (J2SE 1.2) — Swing, Collections Framework
       │
2004: Java 5.0 — Generics, Annotations, Autoboxing, Enums
       │
2010: Oracle acquires Sun Microsystems
       │
2014: Java 8 — Lambda expressions, Stream API
       │
2017→: Six-month release cycle (Java 9, 10, 11...)
```

### 5.4 Java Execution Flow (Platform Independence)

```
                    ┌─────────────────┐
                    │  Java Source     │
                    │  (.java file)   │
                    └────────┬────────┘
                             │ javac (Java Compiler)
                             ↓
                    ┌─────────────────┐
                    │  Bytecode       │
                    │  (.class file)  │
                    └────────┬────────┘
                             │
            ┌────────────────┼────────────────┐
            ↓                ↓                ↓
     ┌──────────┐    ┌──────────┐     ┌──────────┐
     │ JVM on   │    │ JVM on   │     │ JVM on   │
     │ Windows  │    │ Linux    │     │  macOS   │
     └──────────┘    └──────────┘     └──────────┘
            ↓                ↓                ↓
     Machine Code     Machine Code     Machine Code
```

> **Key Point:** Java code is compiled to **bytecode** (platform-independent), which is then interpreted by the **JVM** (platform-specific). This gives Java its "Write Once, Run Anywhere" capability.

---

## 6. The White Paper Description (Java Buzzwords)

James Gosling and Henry McGilton published the original Java White Paper describing 11 key features (buzzwords):

### 6.1 The 11 Buzzwords (Exam Important ⭐)

| # | Buzzword | Description |
|---|----------|-------------|
| 1 | **Simple** | Easy to learn; syntax based on C/C++ but removed complex features (pointers, operator overloading, multiple inheritance) |
| 2 | **Object-Oriented** | Everything is modeled as objects; supports encapsulation, inheritance, polymorphism |
| 3 | **Distributed** | Supports networking through RMI, sockets; designed for distributed internet environment |
| 4 | **Robust** | Strong type checking, exception handling, garbage collection; eliminates crash-prone features |
| 5 | **Secure** | No pointers, bytecode verifier, class loader, security manager; runs in sandboxed JVM |
| 6 | **Architecture-Neutral** | Bytecode runs on any platform with a JVM — not tied to any hardware |
| 7 | **Portable** | "Write Once, Run Anywhere" — same bytecode works on Windows, Linux, Mac |
| 8 | **Interpreted** | Bytecode is interpreted by JVM at runtime (also JIT compiled for performance) |
| 9 | **High-Performance** | JIT (Just-In-Time) compiler converts bytecode to native code for faster execution |
| 10 | **Multithreaded** | Built-in support for multithreading — concurrent execution of programs |
| 11 | **Dynamic** | Supports dynamic loading of classes; classes are loaded on demand at runtime |

### 6.2 Detailed Explanation of Key Buzzwords

#### Simple
```
C/C++ Features REMOVED in Java:
  ✗ Pointers (replaced by references)
  ✗ Operator overloading
  ✗ Multiple inheritance (replaced by interfaces)
  ✗ goto statement
  ✗ Preprocessor (#define, #include)
  ✗ Manual memory management (replaced by garbage collection)
```

#### Robust
```
Java's Robustness Features:
  ✓ Strong type checking at compile-time
  ✓ Exception handling (try-catch-finally)
  ✓ Automatic garbage collection
  ✓ No pointer arithmetic
  ✓ Array bounds checking
  ✓ Null pointer exception handling
```

#### Secure
```
Java Security Model:
┌─────────────────────────────────────┐
│          Java Program               │
│    ┌─────────────────────────┐      │
│    │      JVM Sandbox        │      │
│    │  ┌─────────────────┐    │      │
│    │  │ Class Loader     │   │      │
│    │  │ Bytecode Verifier│   │      │
│    │  │ Security Manager │   │      │
│    │  └─────────────────┘    │      │
│    └─────────────────────────┘      │
└─────────────────────────────────────┘
          ↓ Restricted Access
    ┌─────────────────┐
    │ Operating System │
    └─────────────────┘
```

---

## 7. OOP Concepts (The Four Pillars)

### 7.1 Overview

```
              ┌───────────────────────────┐
              │   Object-Oriented         │
              │   Programming Pillars     │
              └───────────┬───────────────┘
      ┌──────────┬────────┼────────┬──────────┐
      ↓          ↓        ↓        ↓          ↓
┌──────────┐┌────────┐┌────────┐┌──────────┐┌─────────┐
│Encapsu-  ││Abstrac-││Inheri- ││Polymor-  ││ Class & │
│lation    ││tion    ││tance   ││phism     ││ Object  │
└──────────┘└────────┘└────────┘└──────────┘└─────────┘
```

### 7.2 Class and Object

**Class:** A blueprint/template that defines the structure and behavior of objects.

**Object:** An instance of a class — a real entity with state and behavior.

```java
// Class - Blueprint
class Student {
    // Attributes (State)
    String name;
    int rollNo;
    double marks;
    
    // Constructor
    Student(String name, int rollNo, double marks) {
        this.name = name;
        this.rollNo = rollNo;
        this.marks = marks;
    }
    
    // Methods (Behavior)
    void display() {
        System.out.println("Name: " + name);
        System.out.println("Roll No: " + rollNo);
        System.out.println("Marks: " + marks);
    }
    
    String getGrade() {
        if (marks >= 90) return "A+";
        else if (marks >= 80) return "A";
        else if (marks >= 70) return "B";
        else return "C";
    }
}

// Object - Instance
public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Rahul", 101, 92.5);  // Object creation
        Student s2 = new Student("Priya", 102, 85.0);   // Another object
        
        s1.display();  // Message passing
        System.out.println("Grade: " + s1.getGrade());
    }
}
```

```
Memory Representation:
┌────────────┐         ┌──────────────────┐
│ Reference  │         │   Object (Heap)   │
│    s1      │────────→│ name = "Rahul"    │
│            │         │ rollNo = 101      │
└────────────┘         │ marks = 92.5      │
  (Stack)              └──────────────────┘

┌────────────┐         ┌──────────────────┐
│ Reference  │         │   Object (Heap)   │
│    s2      │────────→│ name = "Priya"    │
│            │         │ rollNo = 102      │
└────────────┘         │ marks = 85.0      │
  (Stack)              └──────────────────┘
```

### 7.3 Encapsulation

**Definition:** Wrapping data (variables) and methods (functions) together into a single unit (class), and restricting direct access to internal data.

**Implementation:** Using **private** access modifiers + **getters/setters**

```java
class BankAccount {
    // Private data - cannot be accessed directly
    private double balance;
    private String accountNo;
    
    // Constructor
    public BankAccount(String accountNo, double initialBalance) {
        this.accountNo = accountNo;
        this.balance = initialBalance;
    }
    
    // Getter - controlled read access
    public double getBalance() {
        return balance;
    }
    
    // Public method - controlled write access with validation
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid amount");
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
        } else {
            System.out.println("Invalid withdrawal");
        }
    }
}
```

**Benefits of Encapsulation:**
1. **Data Hiding** — Internal state is protected
2. **Controlled Access** — Through getter/setter methods
3. **Validation** — Can add checks before modifying data
4. **Flexibility** — Internal implementation can change without affecting other code
5. **Maintainability** — Changes are localized to the class

### 7.4 Abstraction

**Definition:** Hiding the complex internal implementation and showing only the essential features to the user.

**Implementation:** Using **abstract classes** and **interfaces**

```java
// Abstract class - provides abstraction
abstract class Shape {
    String color;
    
    // Abstract method - no implementation
    abstract double area();
    abstract double perimeter();
    
    // Concrete method
    void displayColor() {
        System.out.println("Color: " + color);
    }
}

class Circle extends Shape {
    double radius;
    
    Circle(double radius, String color) {
        this.radius = radius;
        this.color = color;
    }
    
    // Providing implementation
    @Override
    double area() {
        return Math.PI * radius * radius;
    }
    
    @Override
    double perimeter() {
        return 2 * Math.PI * radius;
    }
}

class Rectangle extends Shape {
    double length, width;
    
    Rectangle(double length, double width, String color) {
        this.length = length;
        this.width = width;
        this.color = color;
    }
    
    @Override
    double area() {
        return length * width;
    }
    
    @Override
    double perimeter() {
        return 2 * (length + width);
    }
}
```

**Abstraction vs Encapsulation:**

| Abstraction | Encapsulation |
|-------------|---------------|
| Hides implementation **complexity** | Hides **data** |
| Achieved by abstract classes/interfaces | Achieved by access modifiers (private) |
| Design level | Implementation level |
| "What" an object does | "How" it does it |
| Focuses on the outside view | Focuses on the inside view |

### 7.5 Inheritance

**Definition:** A mechanism where a new class (child/subclass) acquires the properties and behaviors of an existing class (parent/superclass).

**Keyword:** `extends`

```java
// Parent/Super class
class Animal {
    String name;
    
    void eat() {
        System.out.println(name + " is eating");
    }
    
    void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Child/Sub class - inherits from Animal
class Dog extends Animal {
    String breed;
    
    void bark() {
        System.out.println(name + " is barking");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.name = "Buddy";    // Inherited attribute
        d.breed = "Labrador"; // Own attribute
        d.eat();              // Inherited method
        d.bark();             // Own method
    }
}
```

**Types of Inheritance:**

```
1. Single Inheritance        2. Multilevel Inheritance
   ┌───────┐                    ┌───────┐
   │   A   │                    │   A   │
   └───┬───┘                    └───┬───┘
       ↓                            ↓
   ┌───────┐                    ┌───────┐
   │   B   │                    │   B   │
   └───────┘                    └───┬───┘
                                    ↓
                                ┌───────┐
                                │   C   │
                                └───────┘

3. Hierarchical Inheritance  4. Multiple Inheritance
   ┌───────┐                  ┌───────┐ ┌───────┐
   │   A   │                  │   A   │ │   B   │
   └───┬───┘                  └───┬───┘ └───┬───┘
    ┌──┴──┐                       ↓         ↓
    ↓     ↓                   ┌───────────────┐
┌──────┐┌──────┐              │      C        │
│  B   ││  C   │              └───────────────┘
└──────┘└──────┘              (NOT supported with
                               classes in Java;
                               use interfaces)
```

### 7.6 Polymorphism

**Definition:** The ability of an object to take many forms. Same method name but different behavior depending on the context.

**Two Types:**

```
           Polymorphism
          ┌─────┴─────┐
   Compile-time     Runtime
  (Static)        (Dynamic)
     │                │
  Method           Method
  Overloading      Overriding
```

#### Compile-time Polymorphism (Method Overloading)
```java
class Calculator {
    // Same method name, different parameters
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

#### Runtime Polymorphism (Method Overriding)
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
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
        Animal a;           // Reference of parent type
        
        a = new Dog();      // Object of child type
        a.sound();          // Output: Dog barks
        
        a = new Cat();
        a.sound();          // Output: Cat meows
    }
}
```

### 7.7 Summary Table of OOP Concepts

| Concept | Definition | Keyword/Mechanism | Example |
|---------|-----------|-------------------|---------|
| **Class** | Blueprint for objects | `class` | `class Student { }` |
| **Object** | Instance of a class | `new` | `Student s = new Student();` |
| **Encapsulation** | Data hiding + bundling | `private`, getters/setters | Private fields with public methods |
| **Abstraction** | Hide complexity | `abstract`, `interface` | Abstract Shape class |
| **Inheritance** | Reuse via parent-child | `extends` | `class Dog extends Animal` |
| **Polymorphism** | Many forms | Overloading/Overriding | Same method, different behavior |

---

## 8. Important Exam Questions

### Short Answer Questions
1. Define Object-Oriented Programming. List its four pillars.
2. What is "Computation as Simulation"?
3. Explain Messages and Methods with example.
4. List the 11 buzzwords (features) of Java.
5. Differentiate between Abstraction and Encapsulation.
6. What is the significance of JVM in Java?

### Long Answer Questions
1. Explain Object-Oriented Thinking with suitable examples. How does it differ from procedural programming?
2. Describe the history of Java. Why was it created and what problems did it solve?
3. Explain the Java White Paper buzzwords in detail with examples.
4. Explain all four pillars of OOP with code examples.
5. Write a Java program demonstrating Encapsulation, Inheritance, and Polymorphism.

---

> **Tip:** For exams, remember the acronym **A PIE** for OOP pillars:
> - **A** — Abstraction
> - **P** — Polymorphism
> - **I** — Inheritance
> - **E** — Encapsulation
