# UNIT 2: Inheritance in Java

---

## 1. Understanding Inheritance — An Intuitive Description

### 1.1 What is Inheritance?

**Inheritance** is a mechanism in OOP where a **new class (child/subclass/derived class)** acquires the properties and behaviors of an **existing class (parent/superclass/base class)**.

It represents the **IS-A relationship**.

```
Real-World Analogy:
┌─────────────────┐
│     Vehicle      │  ← Parent (General)
│  - color         │
│  - speed         │
│  + start()       │
│  + stop()        │
└────────┬────────┘
    ┌────┴────┐
    ↓         ↓
┌──────┐  ┌──────┐
│ Car  │  │ Bike │  ← Children (Specific)
│+gear │  │+kick │
│change│  │Start │
└──────┘  └──────┘

Car IS-A Vehicle ✓
Bike IS-A Vehicle ✓
```

### 1.2 Syntax

```java
class SuperClass {
    // parent class members
}

class SubClass extends SuperClass {
    // child class members + inherited members
}
```

### 1.3 What is Inherited?

| Inherited | NOT Inherited |
|-----------|---------------|
| Public members | Private members (accessible only via public methods) |
| Protected members | Constructors (but can be called using `super()`) |
| Default members (same package) | Static members (belong to class, not inherited in true sense) |

---

## 2. The Base Class: Object

### 2.1 The `java.lang.Object` Class

In Java, **every class implicitly extends `java.lang.Object`**. It is the root of the class hierarchy.

```
        ┌──────────────┐
        │ java.lang.   │
        │ Object       │  ← Root of ALL Java classes
        └──────┬───────┘
     ┌─────────┼─────────┐
     ↓         ↓         ↓
  String    Animal    YourClass
     ↓
  MyClass
```

### 2.2 Methods of Object Class (Exam Important ⭐)

| Method | Description |
|--------|-------------|
| `toString()` | Returns string representation of the object |
| `equals(Object obj)` | Checks if two objects are equal |
| `hashCode()` | Returns hash code value of the object |
| `getClass()` | Returns the runtime class of the object |
| `clone()` | Creates and returns a copy of the object |
| `finalize()` | Called by garbage collector before object destruction |
| `notify()` | Wakes up a single waiting thread |
| `notifyAll()` | Wakes up all waiting threads |
| `wait()` | Causes current thread to wait |

```java
class Student {
    String name;
    int rollNo;
    
    Student(String name, int rollNo) {
        this.name = name;
        this.rollNo = rollNo;
    }
    
    // Overriding Object's toString()
    @Override
    public String toString() {
        return "Student[name=" + name + ", rollNo=" + rollNo + "]";
    }
    
    // Overriding Object's equals()
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Student s = (Student) obj;
        return rollNo == s.rollNo && name.equals(s.name);
    }
}
```

---

## 3. Subclass, Subtype, and Substitutability

### 3.1 Subclass vs Subtype

| Subclass | Subtype |
|----------|---------|
| Created using `extends` keyword | A subclass that follows the **Liskov Substitution Principle (LSP)** |
| Inherits code from parent | Can be used **anywhere** the parent type is expected |
| Structural relationship | Behavioral relationship |
| All subtypes are subclasses | NOT all subclasses are subtypes |

### 3.2 Liskov Substitution Principle (LSP)

> If S is a subtype of T, then objects of type T can be replaced with objects of type S **without altering the correctness** of the program.

```java
// Good Example (Subtype) ✓
class Bird {
    void fly() { System.out.println("Flying"); }
}
class Sparrow extends Bird {
    @Override
    void fly() { System.out.println("Sparrow flying"); }
}
// Sparrow can substitute Bird everywhere — it IS a subtype

// Bad Example (Subclass but NOT Subtype) ✗
class Penguin extends Bird {
    @Override
    void fly() { 
        throw new UnsupportedOperationException("Penguins can't fly!");
    }
}
// Penguin breaks the contract — it is a subclass but NOT a subtype
```

### 3.3 Substitutability

```java
// Parent reference can hold child object
Bird b = new Sparrow();  // Substitutability
b.fly();  // Output: Sparrow flying (runtime polymorphism)
```

---

## 4. Forms of Inheritance (Exam Important ⭐)

### 4.1 Types of Inheritance in Java

```
1. SINGLE INHERITANCE          2. MULTILEVEL INHERITANCE
   ┌─────┐                       ┌─────┐
   │  A  │                       │  A  │ (Grandparent)
   └──┬──┘                       └──┬──┘
      ↓                              ↓
   ┌─────┐                       ┌─────┐
   │  B  │                       │  B  │ (Parent)
   └─────┘                       └──┬──┘
                                     ↓
                                  ┌─────┐
                                  │  C  │ (Child)
                                  └─────┘

3. HIERARCHICAL INHERITANCE    4. MULTIPLE INHERITANCE
   ┌─────┐                     ┌─────┐   ┌─────┐
   │  A  │                     │  A  │   │  B  │
   └──┬──┘                     └──┬──┘   └──┬──┘
   ┌──┴──┐                        └───┬───┘
   ↓     ↓                        ┌───────┐
┌─────┐┌─────┐                    │   C   │
│  B  ││  C  │                    └───────┘
└─────┘└─────┘              (NOT with classes,
                              ONLY via interfaces)

5. HYBRID INHERITANCE
   Combination of two or more types
   (Achieved using interfaces in Java)
```

### 4.2 Single Inheritance
```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}
```

### 4.3 Multilevel Inheritance
```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}

class Puppy extends Dog {
    void play() { System.out.println("Playing"); }
}
// Puppy → Dog → Animal (3 levels)
```

### 4.4 Hierarchical Inheritance
```java
class Shape {
    void draw() { System.out.println("Drawing shape"); }
}

class Circle extends Shape {
    void draw() { System.out.println("Drawing circle"); }
}

class Rectangle extends Shape {
    void draw() { System.out.println("Drawing rectangle"); }
}
// Both Circle and Rectangle extend Shape
```

### 4.5 Why No Multiple Inheritance with Classes?

**The Diamond Problem:**
```
        ┌─────┐
        │  A  │  void display()
        └──┬──┘
       ┌───┴───┐
       ↓       ↓
    ┌─────┐ ┌─────┐
    │  B  │ │  C  │  Both override display()
    └──┬──┘ └──┬──┘
       └───┬───┘
        ┌─────┐
        │  D  │  Which display() to use?? AMBIGUITY!
        └─────┘
```

**Solution:** Java supports multiple inheritance through **interfaces** (not classes).

```java
interface Printable {
    void print();
}

interface Showable {
    void show();
}

class Document implements Printable, Showable {
    public void print() { System.out.println("Printing"); }
    public void show() { System.out.println("Showing"); }
}
```

---

## 5. Modifiers and Inheritance

### 5.1 Access Modifiers Effect on Inheritance

| Modifier | Same Class | Same Package | Subclass (diff pkg) | Other Package |
|----------|:----------:|:------------:|:-------------------:|:-------------:|
| `public` | ✓ | ✓ | ✓ | ✓ |
| `protected` | ✓ | ✓ | ✓ | ✗ |
| `default` (no modifier) | ✓ | ✓ | ✗ | ✗ |
| `private` | ✓ | ✗ | ✗ | ✗ |

```java
class Parent {
    public int a = 10;        // Accessible everywhere
    protected int b = 20;     // Accessible in subclass
    int c = 30;               // Default - same package only
    private int d = 40;       // NOT accessible in subclass
}

class Child extends Parent {
    void show() {
        System.out.println(a);  // ✓ public
        System.out.println(b);  // ✓ protected
        System.out.println(c);  // ✓ default (if same package)
        // System.out.println(d); // ✗ ERROR: private
    }
}
```

### 5.2 Non-Access Modifiers

| Modifier | Effect on Inheritance |
|----------|----------------------|
| `final` class | Cannot be extended (no child class) |
| `final` method | Cannot be overridden in child class |
| `static` method | Not truly inherited; can be hidden (not overridden) |
| `abstract` class | Must be extended; cannot be instantiated |
| `abstract` method | Must be overridden in child class |

---

## 6. Benefits of Inheritance (Exam Important ⭐)

| # | Benefit | Description |
|---|---------|-------------|
| 1 | **Code Reusability** | Child class reuses parent class code without rewriting |
| 2 | **Method Overriding** | Child can customize inherited behavior |
| 3 | **Extensibility** | New functionality can be added without modifying existing code |
| 4 | **Polymorphism support** | Parent reference can hold child objects |
| 5 | **Data Hiding** | Parent can hide data from child using `private` |
| 6 | **Reduced Redundancy** | Common code written once in parent |
| 7 | **Logical Organization** | IS-A relationships model real-world hierarchies |

---

## 7. The `final` Keyword

### 7.1 Three Uses of `final`

```
         final
    ┌──────┼──────┐
    ↓      ↓      ↓
Variable  Method  Class
(constant)(no     (no
           override) subclass)
```

### 7.2 final Variable (Constant)
```java
class Circle {
    final double PI = 3.14159;  // Cannot be changed
    
    double area(double r) {
        // PI = 3.14;  // ERROR: cannot assign value to final variable
        return PI * r * r;
    }
}
```

### 7.3 final Method (Cannot Override)
```java
class Parent {
    final void show() {
        System.out.println("Parent's show()");
    }
}

class Child extends Parent {
    // void show() { }  // ERROR: Cannot override final method
    
    void display() {      // ✓ Can add new methods
        System.out.println("Child's display()");
    }
}
```

### 7.4 final Class (Cannot Extend)
```java
final class MathUtils {
    static double square(double x) {
        return x * x;
    }
}

// class AdvancedMath extends MathUtils { }  // ERROR: Cannot extend final class

// Examples of final classes in Java: String, Integer, Math
```

### 7.5 Blank Final Variable
```java
class Student {
    final int rollNo;  // blank final variable
    
    Student(int rollNo) {
        this.rollNo = rollNo;  // Must be initialized in constructor
    }
}
```

---

## 8. The `this` Keyword

### 8.1 Uses of `this`

The `this` keyword refers to the **current object** — the object on which the method is being called.

| Use | Description |
|-----|-------------|
| `this.variable` | Refer to current class's instance variable |
| `this.method()` | Invoke current class's method |
| `this()` | Invoke current class's constructor |
| `return this` | Return current object |
| `this` as argument | Pass current object as argument |

### 8.2 Resolving Ambiguity
```java
class Student {
    String name;
    int age;
    
    // Without 'this' there is ambiguity
    Student(String name, int age) {
        this.name = name;  // this.name = instance variable, name = parameter
        this.age = age;
    }
}
```

### 8.3 Constructor Chaining with `this()`
```java
class Student {
    String name;
    int age;
    String college;
    
    Student() {
        this("Unknown", 0);  // calls 2-arg constructor
        System.out.println("Default constructor");
    }
    
    Student(String name, int age) {
        this(name, age, "Default College");  // calls 3-arg constructor
    }
    
    Student(String name, int age, String college) {
        this.name = name;
        this.age = age;
        this.college = college;
    }
}
```

### 8.4 Returning Current Object
```java
class Builder {
    String name;
    int value;
    
    Builder setName(String name) {
        this.name = name;
        return this;  // returns current object for method chaining
    }
    
    Builder setValue(int value) {
        this.value = value;
        return this;
    }
}

// Usage: Method Chaining
Builder b = new Builder().setName("Test").setValue(42);
```

---

## 9. The `super` Keyword

### 9.1 Uses of `super`

The `super` keyword refers to the **immediate parent class** object.

| Use | Description |
|-----|-------------|
| `super.variable` | Access parent class's variable |
| `super.method()` | Invoke parent class's method |
| `super()` | Invoke parent class's constructor |

### 9.2 Calling Super Class Constructor
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
        super(name);    // MUST be the FIRST statement
        this.breed = breed;
        System.out.println("Dog constructor: " + breed);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog d = new Dog("Buddy", "Labrador");
    }
}
/* Output:
   Animal constructor: Buddy
   Dog constructor: Labrador
*/
```

### 9.3 Accessing Parent's Variable
```java
class Parent {
    int x = 10;
}

class Child extends Parent {
    int x = 20;  // Hides parent's x
    
    void show() {
        System.out.println("Child x = " + x);         // 20
        System.out.println("Parent x = " + super.x);  // 10
    }
}
```

### 9.4 Accessing Parent's Method
```java
class Animal {
    void display() {
        System.out.println("I am an Animal");
    }
}

class Dog extends Animal {
    @Override
    void display() {
        super.display();  // Call parent's version FIRST
        System.out.println("I am a Dog");
    }
}

/* Output:
   I am an Animal
   I am a Dog
*/
```

### 9.5 Constructor Chaining with `super()`

```
When Dog object is created:

┌─────────────────────────────┐
│ Dog Constructor called      │
│   ↓                         │
│ super() → Animal Constructor│
│   ↓                         │
│ super() → Object Constructor│  ← Automatically called
│   ↓                         │
│ Object Constructor executes │
│   ↓                         │
│ Animal Constructor executes │
│   ↓                         │
│ Dog Constructor executes    │
└─────────────────────────────┘

Order: Object → Animal → Dog (top-down execution)
```

> **Important Rule:** `super()` must be the **first statement** in the constructor. You cannot use both `this()` and `super()` in the same constructor.

---

## 10. Method Overriding (Exam Important ⭐)

### 10.1 Definition

When a subclass provides a **specific implementation** for a method that is **already defined** in its parent class, it is called **method overriding**.

### 10.2 Rules of Method Overriding

| Rule | Description |
|------|-------------|
| Same method name | Must have exact same name |
| Same parameters | Must have exact same parameter list |
| Same or covariant return type | Return type must be same or a subtype |
| IS-A relationship required | Must be in parent-child relationship |
| Access modifier | Cannot be more restrictive (public → private ✗) |
| `final` methods | Cannot be overridden |
| `static` methods | Cannot be overridden (can be hidden) |
| `private` methods | Cannot be overridden (not inherited) |
| Constructors | Cannot be overridden |

### 10.3 Example
```java
class Shape {
    void draw() {
        System.out.println("Drawing a shape");
    }
    
    double area() {
        return 0;
    }
}

class Circle extends Shape {
    double radius;
    
    Circle(double radius) {
        this.radius = radius;
    }
    
    @Override  // Annotation indicating override
    void draw() {
        System.out.println("Drawing a Circle with radius " + radius);
    }
    
    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    double length, width;
    
    Rectangle(double l, double w) {
        this.length = l;
        this.width = w;
    }
    
    @Override
    void draw() {
        System.out.println("Drawing Rectangle " + length + "x" + width);
    }
    
    @Override
    double area() {
        return length * width;
    }
}
```

### 10.4 Method Overloading vs Method Overriding

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| **Definition** | Same name, different parameters | Same name, same parameters |
| **Class** | Within same class | Between parent-child classes |
| **Parameters** | Must be different | Must be same |
| **Return type** | Can be different | Must be same or covariant |
| **Binding** | Compile-time (static) | Runtime (dynamic) |
| **`static` methods** | Can be overloaded | Cannot be overridden |
| **`final` methods** | Can be overloaded | Cannot be overridden |
| **Access modifier** | No restriction | Cannot be more restrictive |
| **Performance** | Faster (compile-time) | Slower (runtime lookup) |

---

## 11. Dynamic Method Dispatch (Runtime Polymorphism) (Exam Important ⭐)

### 11.1 Definition

Dynamic Method Dispatch is the mechanism by which a call to an **overridden method** is resolved at **runtime** rather than compile-time. It is the basis for **runtime polymorphism** in Java.

### 11.2 How it Works

```
                    Compile Time         Runtime
                    ┌──────────┐        ┌──────────┐
Animal a = new Dog();                    
     ↑         ↑    │Reference │        │ Actual   │
     │         │    │type:     │        │ Object:  │
     │         │    │ Animal   │        │ Dog      │
     │         │    └──────────┘        └──────────┘
     │         │
  Reference   Actual
  Type        Object

a.sound();  → JVM checks the ACTUAL OBJECT (Dog) at RUNTIME
             → Calls Dog's sound() method
```

### 11.3 Complete Example
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks: Woof!");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Cat meows: Meow!");
    }
}

class Duck extends Animal {
    @Override
    void sound() {
        System.out.println("Duck quacks: Quack!");
    }
}

public class DynamicDispatchDemo {
    public static void main(String[] args) {
        Animal a;  // Parent reference
        
        a = new Dog();
        a.sound();  // Output: Dog barks: Woof!
        
        a = new Cat();
        a.sound();  // Output: Cat meows: Meow!
        
        a = new Duck();
        a.sound();  // Output: Duck quacks: Quack!
        
        // Array of parent type holding different child objects
        Animal[] animals = { new Dog(), new Cat(), new Duck() };
        for (Animal animal : animals) {
            animal.sound();  // Each calls its own version
        }
    }
}
```

### 11.4 Why Dynamic Dispatch is Important

1. **Flexibility** — Same code works with different types
2. **Extensibility** — New subclasses can be added without changing existing code
3. **Maintainability** — One interface, many implementations
4. **Foundation of Design Patterns** — Strategy, Template Method, etc.

---

## 12. Using Abstract Classes

### 12.1 Definition

An **abstract class** is a class that:
- **Cannot be instantiated** (cannot create objects)
- **May contain abstract methods** (methods without body)
- **May contain concrete methods** (methods with body)
- Declared using the `abstract` keyword

### 12.2 Rules

| Rule | Description |
|------|-------------|
| Cannot be instantiated | `new AbstractClass()` → ERROR |
| Can have constructors | Called when child object is created |
| Can have abstract methods | Must be overridden by child |
| Can have concrete methods | Inherited by child as-is |
| Can have instance variables | Both regular and final |
| Child MUST override all abstract methods | Unless child is also abstract |
| Can have `static` methods | Yes |
| Can have `final` methods | Yes (cannot be overridden) |

### 12.3 Complete Example
```java
// Abstract Class
abstract class Shape {
    String color;
    
    // Constructor
    Shape(String color) {
        this.color = color;
    }
    
    // Abstract methods - MUST be overridden
    abstract double area();
    abstract double perimeter();
    
    // Concrete method - inherited as-is
    void displayColor() {
        System.out.println("Color: " + color);
    }
    
    @Override
    public String toString() {
        return "Shape[color=" + color + ", area=" + area() + "]";
    }
}

class Circle extends Shape {
    double radius;
    
    Circle(double radius, String color) {
        super(color);
        this.radius = radius;
    }
    
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
        super(color);
        this.length = length;
        this.width = width;
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

class Triangle extends Shape {
    double a, b, c;  // sides
    double height;
    
    Triangle(double a, double b, double c, double height, String color) {
        super(color);
        this.a = a; this.b = b; this.c = c;
        this.height = height;
    }
    
    @Override
    double area() {
        return 0.5 * a * height;
    }
    
    @Override
    double perimeter() {
        return a + b + c;
    }
}

public class AbstractDemo {
    public static void main(String[] args) {
        // Shape s = new Shape("Red"); // ERROR: Cannot instantiate abstract class
        
        Shape s1 = new Circle(5, "Red");
        Shape s2 = new Rectangle(4, 6, "Blue");
        Shape s3 = new Triangle(3, 4, 5, 4, "Green");
        
        Shape[] shapes = {s1, s2, s3};
        for (Shape s : shapes) {
            s.displayColor();
            System.out.println("Area: " + s.area());
            System.out.println("Perimeter: " + s.perimeter());
            System.out.println();
        }
    }
}
```

### 12.4 Abstract Class vs Interface

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| **Keyword** | `abstract` | `interface` |
| **Methods** | Abstract + Concrete | Abstract only (Java 7); default + static (Java 8+) |
| **Variables** | Any type | Only `public static final` |
| **Constructor** | Can have | Cannot have |
| **Multiple inheritance** | Single only | Multiple allowed |
| **Access modifiers** | Any | Public only (methods) |
| **Speed** | Faster | Slightly slower |
| **When to use** | Shared code among related classes | Unrelated classes need common behavior |

---

## 13. Using `final` with Inheritance

### 13.1 Final Class — Prevent Inheritance
```java
final class ImmutableClass {
    final int value;
    
    ImmutableClass(int value) {
        this.value = value;
    }
    
    int getValue() {
        return value;
    }
}

// class Child extends ImmutableClass { }  // COMPILE ERROR!
```

### 13.2 Final Method — Prevent Overriding
```java
class Payment {
    // template method - cannot be changed by subclass
    final void processPayment(double amount) {
        validate(amount);
        deduct(amount);
        sendReceipt();
    }
    
    void validate(double amount) {
        System.out.println("Validating amount: " + amount);
    }
    
    void deduct(double amount) {
        System.out.println("Deducting: " + amount);
    }
    
    void sendReceipt() {
        System.out.println("Receipt sent");
    }
}

class CreditCardPayment extends Payment {
    @Override
    void validate(double amount) {
        System.out.println("Validating credit card for: " + amount);
    }
    
    // Cannot override processPayment() — it's final!
}
```

### 13.3 Why Use Final?

| Purpose | Use |
|---------|-----|
| **Security** | Prevent malicious subclasses from altering behavior |
| **Design** | Ensure critical methods are not changed |
| **Optimization** | JVM can inline final methods for better performance |
| **Immutability** | Create immutable classes (e.g., `String`) |

---

## 14. Important Exam Questions

### Short Answer Questions
1. What is inheritance? List its types in Java.
2. Why does Java not support multiple inheritance with classes?
3. Differentiate between method overloading and method overriding.
4. What is Dynamic Method Dispatch? Explain with example.
5. List the methods of the Object class.
6. What are the three uses of `final` keyword?
7. Differentiate between `this` and `super` keyword.

### Long Answer Questions
1. Explain all forms of inheritance with diagrams and Java code examples.
2. What is method overriding? Explain its rules and write a program demonstrating it.
3. Explain Dynamic Method Dispatch with a complete Java program.
4. What are abstract classes? How are they different from interfaces? Explain with example.
5. Explain `super` keyword with all its uses with code examples.
6. Write a Java program that demonstrates multilevel inheritance, method overriding, and use of `super`.
7. Explain the benefits of inheritance. How does `final` keyword affect inheritance?

---

> **Exam Tip:** Always remember the constructor chain: when creating a child object, constructors are called from **top to bottom** (Object → Parent → Child), but each constructor's body executes after calling `super()`.
