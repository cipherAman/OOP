# Detailed OOP & Java Differences (Exam Focus)

---

### 1. POP (Procedural) vs. OOP (Object-Oriented)
| Feature | POP (e.g., C, Pascal) | OOP (e.g., C++, Java, Python) |
| :--- | :--- | :--- |
| **Approach** | Top-down approach. | Bottom-up approach. |
| **Focus** | Focuses on functions/procedures and logical sequence. | Focuses on data and objects. |
| **Data Hiding** | No data hiding; data can be accessed globally. | Supports data hiding (Encapsulation). |
| **Overloading** | Neither operator nor method overloading is supported. | Supports both method and operator overloading. |
| **Complexity** | Becomes highly complex in large programs. | Easier to manage large, complex software. |

---

### 2. Class vs. Object
| Feature | Class | Object |
| :--- | :--- | :--- |
| **Definition** | A blueprint or template from which objects are created. | An instance of a class; a real-world entity. |
| **Allocation** | No memory is allocated when a class is created. | Memory is allocated when an object is instantiated. |
| **Existence** | Logical existence. | Physical existence. |
| **Declaration** | Declared once (e.g., `class Student { }`). | Created many times (e.g., `Student s1 = new Student()`). |

---

### 3. Method Overloading vs. Method Overriding
| Feature | Method Overloading (Compile-time) | Method Overriding (Run-time) |
| :--- | :--- | :--- |
| **Location** | Occurs within the **same class**. | Occurs between **two classes** (parent and child) with IS-A relationship. |
| **Signature** | Methods must have the **same name** but **different parameters**. | Methods must have the **exact same name and parameters**. |
| **Return Type** | Can be different, but doesn't play a role in distinguishing. | Must be the exact same or covariant. |
| **Polymorphism** | Example of Compile-time (Static) Polymorphism. | Example of Run-time (Dynamic) Polymorphism. |
| **Annotation** | No specific keyword needed. | Usually annotated with `@Override` in Java. |

---

### 4. Abstract Class vs. Interface
| Feature | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Methods** | Can have both abstract (unimplemented) and concrete methods. | Only has abstract methods (until Java 8 introduced default/static). |
| **Variables** | Can have `final`, `non-final`, `static`, and `non-static` variables. | Variables are `public static final` by default (i.e., constants). |
| **Inheritance** | A class can `extend` only ONE abstract class. | A class can `implement` MULTIPLE interfaces. |
| **Constructors** | Can have constructors. | Cannot have constructors. |
| **Access levels** | Can have private, protected, default, public. | Methods are `public abstract` by default. |

---

### 5. `throw` vs. `throws` (Exception Handling)
| Feature | `throw` | `throws` |
| :--- | :--- | :--- |
| **Usage** | Used to explicitly throw a single exception from within a method. | Used in the method signature to declare that the method might throw. |
| **Location** | Used **inside** the method body. | Used **with the method signature**. |
| **Exceptions** | Can throw only one exception at a time. | Can declare multiple exceptions separated by commas. |
| **Syntax** | Followed by an instance variable (object) of the Exception class. | Followed by Exception class names. |

---

### 6. Checked vs. Unchecked Exceptions
| Feature | Checked Exceptions | Unchecked Exceptions |
| :--- | :--- | :--- |
| **Verification** | Checked by the compiler at Compile-Time. | Not checked at compile-time; occur entirely at Run-Time. |
| **Handling** | Must be either caught (`try-catch`) or declared (`throws`). | No strict requirement to handle them, though good practice. |
| **Base Class** | Extend `java.lang.Exception` (excluding `RuntimeException`). | Extend `java.lang.RuntimeException`. |
| **Examples** | `IOException`, `SQLException`, `ClassNotFoundException`. | `NullPointerException`, `ArithmeticException`. |

---

### 7. `final`, `finally`, and `finalize`
| Feature | `final` | `finally` | `finalize()` |
| :--- | :--- | :--- | :--- |
| **Type** | Access modifier keyword. | Block associated with `try-catch`. | Method defined in the `Object` class. |
| **Purpose**| Restricts inheritance, overriding, and reassignment. | Code that **always executes** (cleanup, closing DB connections). | Invoked by GC just before an object is destroyed for cleanup. |
| **Execution**| Executed continuously as per application logic. | Executed after `try` or `catch` block execution. | Executed asynchronously by GC thread. |

---

### 8. `String` vs. `StringBuffer` vs. `StringBuilder`
| Feature | `String` | `StringBuffer` | `StringBuilder` |
| :--- | :--- | :--- | :--- |
| **Mutability** | Immutable. | Mutable. | Mutable. |
| **Safety**| Not thread-safe (safe essentially due to immutability). | Thread-safe (synchronized). | Not thread-safe (not synchronized). |
| **Speed** | Slow when concatenating (creates new objects). | Slower than StringBuilder due to synchronization. | Fast and most efficient for single thread. |
| **Memory** | String Pool or Heap memory. | Heap memory only. | Heap memory only. |

---

### 9. Arrays vs. Vectors (or ArrayLists)
| Feature | Array | Vector / ArrayList |
| :--- | :--- | :--- |
| **Size** | Fixed size defined during creation. Cannot grow/shrink. | Dynamic size. Can grow/shrink automatically. |
| **Types** | Can store both primitives (int, char) and Objects. | Can only store Objects (primitives are autoboxed). |
| **Methods** | No utility methods; only a `length` property. | Rich utility methods: `add()`, `remove()`, `size()`, `contains()`. |
| **Memory** | Less memory intensive. | More memory overhead due to dynamic resizing. |

---

### 10. `Thread` Class vs. `Runnable` Interface
| Feature | Extending `Thread` Class | Implementing `Runnable` Interface |
| :--- | :--- | :--- |
| **Inheritance** | Cannot extend any other class. | Can extend another class since it only implements an interface. |
| **Resources** | Each thread creates a unique object; hard to share resources. | Multiple threads can share the same `Runnable` object. |
| **OOP Design**| Tightly couples the task with the thread mechanism. | Better design; separates the task (Runnable) from the runner (Thread). |

---

### 11. `yield()`, `sleep()`, and `wait()`
| Feature | `sleep(time)` | `yield()` | `wait()` |
| :--- | :--- | :--- | :--- |
| **Purpose** | Pauses the thread for a specified duration. | Hints scheduler to yield current processor use. | Thread waits until another invokes `notify()` or `notifyAll()`. |
| **Lock** | Does **not** release the monitor/lock. | Does **not** release the monitor/lock. | **Releases** the monitor/lock. |
| **Class** | `Thread` class. | `Thread` class. | `Object` class. |
| **Context** | Anywhere. | Anywhere. | Must be within a **synchronized** block/method. |

---

### 12. AWT vs. Swing
| Feature | AWT | Swing |
| :--- | :--- | :--- |
| **Nature** | Heavyweight components (rely on OS). | Lightweight components (written entirely in Java). |
| **Platform**| Platform-dependent appearance. | Platform-independent appearance (Pluggable look and feel). |
| **Speed** | Faster execution (uses OS peers). | Slightly slower compared to AWT. |
| **MVC** | Does not follow Model-View-Controller pattern. | Strictly follows MVC pattern. |
| **Package** | `java.awt.*` | `javax.swing.*` |

---
**Exam Tips:**
1. **Diagrams:** Whenever explaining differences (like Class vs Object or Architecture), drawing a block diagram yields extra marks.
2. **Examples:** Always wrap descriptions of OOP pillars with a short 3-line example (ex: writing `class Animal { }` to show abstraction/inheritance).
3. **Tabular Format:** Present differences purely in tables as shown above; evaluators prefer clear comparative points over paragraphs.
