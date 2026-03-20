# UNIT 5: Polymorphism, AWT, Applets, Event Handling & Swing

---

## PART A: POLYMORPHISM

---

## 1. Varieties of Polymorphism (Exam Important ⭐)

### 1.1 Definition

**Polymorphism** = "Many Forms" — the ability of an entity to take multiple forms.

### 1.2 Classification

```
                    Polymorphism
                   ┌──────┴──────┐
            Compile-Time     Runtime
            (Static)         (Dynamic)
            ┌────┴────┐      ┌────┴────┐
        Overloading  Operator  Over-   Abstract
                   Overloading riding  Methods
                   (NOT in Java)
```

### 1.3 Four Varieties of Polymorphism

| Type | Description | Binding | Example |
|------|-------------|---------|---------|
| **Overloading** | Same name, different parameters | Compile-time | `add(int)`, `add(double)` |
| **Overriding** | Subclass redefines parent method | Runtime | Method in child replaces parent |
| **Pure Polymorphism** | Single interface, multiple implementations | Runtime | Abstract method in parent |
| **Parametric** | Generics (works with any type) | Compile-time | `List<T>` |

---

## 2. Polymorphic Variables

### 2.1 Definition

A **polymorphic variable** is a variable that can hold objects of **different types** at different times during execution. In Java, a **parent reference** can hold a **child object**.

```java
// 'a' is a polymorphic variable
Animal a;           // Declared as Animal

a = new Dog();      // Holds Dog object
a.sound();          // Dog's sound()

a = new Cat();      // NOW holds Cat object
a.sound();          // Cat's sound()

a = new Animal();   // Can also hold Animal
a.sound();          // Animal's sound()
```

### 2.2 Types of Polymorphic Variables

| Type | Description | Example |
|------|-------------|---------|
| **Simple** | Variable of parent type | `Animal a = new Dog();` |
| **Receiver** | `this` inside a method | Implicit polymorphic variable |
| **Parameter** | Method parameter of parent type | `void feed(Animal a)` |
| **Collection** | Collections of parent type | `List<Animal> animals` |

```java
class Zoo {
    // Polymorphic parameter
    void makeSound(Animal a) {
        a.sound();  // Calls actual object's method
    }
    
    void allSounds(Animal[] animals) {
        for (Animal a : animals) {
            a.sound();  // Different sound for each animal
        }
    }
}

Zoo zoo = new Zoo();
zoo.makeSound(new Dog());  // "Woof"
zoo.makeSound(new Cat());  // "Meow"
```

---

## 3. Overloading (Compile-time Polymorphism)

### 3.1 Method Overloading

Same method name but **different parameter lists** in the **same class**.

```java
class MathUtils {
    // Overloaded add methods
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
    
    int add(int a, int b, int c) {
        return a + b + c;
    }
    
    String add(String a, String b) {
        return a + b;  // String concatenation
    }
}
```

### 3.2 Constructor Overloading

```java
class Student {
    String name;
    int age;
    String college;
    
    Student() {
        this("Unknown", 0, "N/A");
    }
    
    Student(String name) {
        this(name, 0, "N/A");
    }
    
    Student(String name, int age) {
        this(name, age, "N/A");
    }
    
    Student(String name, int age, String college) {
        this.name = name;
        this.age = age;
        this.college = college;
    }
}
```

### 3.3 Rules for Overloading

| Can Differ | Cannot Differ (alone) |
|-----------|----------------------|
| Number of parameters | Return type only |
| Type of parameters | Access modifier only |
| Order of parameters | |

---

## 4. Overriding (Runtime Polymorphism)

### 4.1 Complete Example with Upcasting

```java
class Vehicle {
    void start() {
        System.out.println("Vehicle starts");
    }
    
    void fuelType() {
        System.out.println("Generic fuel");
    }
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car starts with key ignition");
    }
    
    @Override
    void fuelType() {
        System.out.println("Petrol/Diesel");
    }
}

class ElectricCar extends Vehicle {
    @Override
    void start() {
        System.out.println("Electric car starts with button");
    }
    
    @Override
    void fuelType() {
        System.out.println("Electric battery");
    }
}

public class OverrideDemo {
    // Polymorphic method
    static void startVehicle(Vehicle v) {
        v.start();        // Calls actual object's method
        v.fuelType();
    }
    
    public static void main(String[] args) {
        startVehicle(new Vehicle());      // Vehicle starts
        startVehicle(new Car());          // Car starts with key ignition
        startVehicle(new ElectricCar());  // Electric car starts with button
    }
}
```

---

## 5. Abstract Methods

### 5.1 Concept

An **abstract method** has **no body** — only a signature. Subclasses **must** provide the implementation.

```java
abstract class Payment {
    String payerName;
    double amount;
    
    Payment(String name, double amount) {
        this.payerName = name;
        this.amount = amount;
    }
    
    // Abstract methods - MUST be implemented
    abstract void processPayment();
    abstract String getPaymentMode();
    
    // Concrete method
    void displayDetails() {
        System.out.println("Payer: " + payerName);
        System.out.println("Amount: Rs." + amount);
        System.out.println("Mode: " + getPaymentMode());
    }
}

class CreditCardPayment extends Payment {
    String cardNumber;
    
    CreditCardPayment(String name, double amount, String cardNumber) {
        super(name, amount);
        this.cardNumber = cardNumber;
    }
    
    @Override
    void processPayment() {
        System.out.println("Processing credit card payment...");
        System.out.println("Card: " + cardNumber);
    }
    
    @Override
    String getPaymentMode() {
        return "Credit Card";
    }
}

class UPIPayment extends Payment {
    String upiId;
    
    UPIPayment(String name, double amount, String upiId) {
        super(name, amount);
        this.upiId = upiId;
    }
    
    @Override
    void processPayment() {
        System.out.println("Processing UPI payment...");
        System.out.println("UPI ID: " + upiId);
    }
    
    @Override
    String getPaymentMode() {
        return "UPI";
    }
}
```

---

## 6. Pure Polymorphism

**Pure Polymorphism** occurs when a **single function** can work with arguments of **many different types**.

```java
abstract class Shape {
    abstract double area();
    abstract void draw();
}

// Single function works with ALL shapes
void processShape(Shape s) {   // Pure polymorphism
    s.draw();
    System.out.println("Area: " + s.area());
}

// Works with Circle, Rectangle, Triangle — any Shape subclass
processShape(new Circle(5));
processShape(new Rectangle(4, 6));
processShape(new Triangle(3, 4, 5));
```

---

## PART B: THE AWT (Abstract Window Toolkit)

---

## 7. AWT Overview

### 7.1 What is AWT?

**AWT (Abstract Window Toolkit)** is Java's original **GUI (Graphical User Interface)** framework. It provides classes for creating windows, buttons, menus, and other UI components.

### 7.2 AWT Class Hierarchy (Exam Important ⭐)

```
                        ┌──────────────┐
                        │    Object    │
                        └──────┬───────┘
                               ↓
                        ┌──────────────┐
                        │  Component   │ ← Base for all GUI components
                        └──────┬───────┘
         ┌───────┬───────┬─────┼──────┬────────┬──────────┐
         ↓       ↓       ↓     ↓      ↓        ↓          ↓
     ┌──────┐┌──────┐┌──────┐┌────┐┌──────┐┌────────┐┌────────┐
     │Button││Label ││Text  ││List││Check ││TextArea││Canvas  │
     │      ││      ││Field ││    ││box   ││        ││        │
     └──────┘└──────┘└──────┘└────┘└──────┘└────────┘└────────┘
                                    
                        ┌──────────────┐
                        │  Container   │ ← Can hold other components
                        └──────┬───────┘
                   ┌───────────┼───────────┐
                   ↓           ↓           ↓
              ┌──────┐   ┌──────────┐ ┌────────┐
              │Panel │   │ Window   │ │ScrollPane│
              └──────┘   └────┬─────┘ └────────┘
                        ┌─────┴─────┐
                        ↓           ↓
                   ┌──────┐   ┌──────────┐
                   │Frame │   │ Dialog   │
                   └──────┘   └──────────┘
```

### 7.3 Key AWT Classes

| Class | Description |
|-------|-------------|
| **Component** | Abstract base class for all GUI components |
| **Container** | A component that can contain other components |
| **Frame** | Top-level window with title bar and borders |
| **Panel** | Simple container for organizing components |
| **Window** | Top-level window without title bar |
| **Dialog** | Pop-up window for user interaction |
| **Canvas** | Blank drawing area |
| **Button** | Clickable button |
| **Label** | Non-editable text |
| **TextField** | Single-line text input |
| **TextArea** | Multi-line text input |
| **Checkbox** | Toggle checkbox |
| **Choice** | Drop-down menu |
| **List** | Scrollable list of items |
| **MenuBar** | Menu bar for a frame |

---

## 8. Layout Managers

### 8.1 What is a Layout Manager?

A **Layout Manager** determines how components are arranged inside a container.

### 8.2 Types of Layout Managers (Exam Important ⭐)

```
1. FlowLayout (default for Panel)
┌────────────────────────────────┐
│ [Btn1] [Btn2] [Btn3] [Btn4]   │
│ [Btn5] [Btn6]                  │
└────────────────────────────────┘
Components flow left to right, wrap to next row

2. BorderLayout (default for Frame)
┌────────────────────────────────┐
│           NORTH                │
├──────┬──────────────┬──────────┤
│      │              │          │
│ WEST │   CENTER     │   EAST   │
│      │              │          │
├──────┴──────────────┴──────────┤
│           SOUTH                │
└────────────────────────────────┘
5 regions: North, South, East, West, Center

3. GridLayout
┌────────┬────────┬────────┐
│  Btn1  │  Btn2  │  Btn3  │
├────────┼────────┼────────┤
│  Btn4  │  Btn5  │  Btn6  │
└────────┴────────┴────────┘
Equal-sized grid cells (rows × columns)

4. CardLayout
Shows one "card" at a time:
┌──────────────────┐  ┌──────────────────┐
│    Card 1        │  │    Card 2        │
│  (visible)       │  │  (hidden)        │
└──────────────────┘  └──────────────────┘

5. GridBagLayout
Complex flexible grid (most powerful)
```

### 8.3 Example

```java
import java.awt.*;

public class LayoutDemo extends Frame {
    LayoutDemo() {
        setTitle("Layout Manager Demo");
        setSize(400, 300);
        
        // Using BorderLayout (default for Frame)
        setLayout(new BorderLayout());
        
        add(new Button("North"), BorderLayout.NORTH);
        add(new Button("South"), BorderLayout.SOUTH);
        add(new Button("East"), BorderLayout.EAST);
        add(new Button("West"), BorderLayout.WEST);
        add(new Button("Center"), BorderLayout.CENTER);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new LayoutDemo();
    }
}
```

---

## 9. User Interface Components

### 9.1 Creating Basic UI

```java
import java.awt.*;
import java.awt.event.*;

public class UIComponentDemo extends Frame {
    Label nameLabel, resultLabel;
    TextField nameField;
    Button submitBtn, clearBtn;
    Checkbox checkBox;
    Choice choice;
    TextArea textArea;
    
    UIComponentDemo() {
        setTitle("AWT Components Demo");
        setSize(500, 400);
        setLayout(new FlowLayout());
        
        // Label
        nameLabel = new Label("Enter Name: ");
        add(nameLabel);
        
        // TextField
        nameField = new TextField(20);
        add(nameField);
        
        // Buttons
        submitBtn = new Button("Submit");
        clearBtn = new Button("Clear");
        add(submitBtn);
        add(clearBtn);
        
        // Checkbox
        checkBox = new Checkbox("I agree to terms");
        add(checkBox);
        
        // Choice (Dropdown)
        choice = new Choice();
        choice.add("Java");
        choice.add("Python");
        choice.add("C++");
        add(choice);
        
        // TextArea
        textArea = new TextArea(5, 30);
        add(textArea);
        
        // Result Label
        resultLabel = new Label("Result will appear here");
        add(resultLabel);
        
        // Button Action
        submitBtn.addActionListener(e -> {
            String name = nameField.getText();
            String lang = choice.getSelectedItem();
            boolean agreed = checkBox.getState();
            resultLabel.setText("Name: " + name + ", Lang: " + lang + 
                              ", Agreed: " + agreed);
        });
        
        clearBtn.addActionListener(e -> {
            nameField.setText("");
            textArea.setText("");
            resultLabel.setText("Cleared");
        });
        
        // Window Close
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                dispose();
                System.exit(0);
            }
        });
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new UIComponentDemo();
    }
}
```

---

## 10. Panels and Dialogs

### 10.1 Panel

A **Panel** is a container that can hold other components. Used to organize UI.

```java
import java.awt.*;

public class PanelDemo extends Frame {
    PanelDemo() {
        setTitle("Panel Demo");
        setSize(400, 300);
        
        // Create panels
        Panel topPanel = new Panel();
        topPanel.setBackground(Color.LIGHT_GRAY);
        topPanel.add(new Label("Top Panel"));
        topPanel.add(new TextField(15));
        topPanel.add(new Button("Search"));
        
        Panel centerPanel = new Panel();
        centerPanel.setLayout(new GridLayout(2, 2));
        centerPanel.add(new Button("Button 1"));
        centerPanel.add(new Button("Button 2"));
        centerPanel.add(new Button("Button 3"));
        centerPanel.add(new Button("Button 4"));
        
        Panel bottomPanel = new Panel();
        bottomPanel.add(new Button("OK"));
        bottomPanel.add(new Button("Cancel"));
        
        // Add panels to frame
        add(topPanel, BorderLayout.NORTH);
        add(centerPanel, BorderLayout.CENTER);
        add(bottomPanel, BorderLayout.SOUTH);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new PanelDemo();
    }
}
```

### 10.2 Dialog

A **Dialog** is a pop-up window that requires user attention.

```java
import java.awt.*;
import java.awt.event.*;

public class DialogDemo extends Frame {
    DialogDemo() {
        setTitle("Dialog Demo");
        setSize(300, 200);
        
        Button showDialog = new Button("Show Dialog");
        add(showDialog);
        
        showDialog.addActionListener(e -> {
            // Create modal dialog
            Dialog d = new Dialog(this, "My Dialog", true);
            d.setSize(200, 150);
            d.setLayout(new FlowLayout());
            d.add(new Label("Are you sure?"));
            
            Button yesBtn = new Button("Yes");
            Button noBtn = new Button("No");
            d.add(yesBtn);
            d.add(noBtn);
            
            yesBtn.addActionListener(ev -> d.dispose());
            noBtn.addActionListener(ev -> d.dispose());
            
            d.setVisible(true);
        });
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new DialogDemo();
    }
}
```

---

## 11. The MenuBar

```java
import java.awt.*;
import java.awt.event.*;

public class MenuBarDemo extends Frame {
    MenuBarDemo() {
        setTitle("Menu Bar Demo");
        setSize(400, 300);
        
        // Create MenuBar
        MenuBar mb = new MenuBar();
        
        // File Menu
        Menu fileMenu = new Menu("File");
        MenuItem newItem = new MenuItem("New");
        MenuItem openItem = new MenuItem("Open");
        MenuItem saveItem = new MenuItem("Save");
        MenuItem exitItem = new MenuItem("Exit");
        
        fileMenu.add(newItem);
        fileMenu.add(openItem);
        fileMenu.add(saveItem);
        fileMenu.addSeparator();
        fileMenu.add(exitItem);
        
        // Edit Menu
        Menu editMenu = new Menu("Edit");
        editMenu.add(new MenuItem("Cut"));
        editMenu.add(new MenuItem("Copy"));
        editMenu.add(new MenuItem("Paste"));
        
        // Sub-menu
        Menu helpMenu = new Menu("Help");
        Menu subMenu = new Menu("Documentation");
        subMenu.add(new MenuItem("API Docs"));
        subMenu.add(new MenuItem("Tutorial"));
        helpMenu.add(subMenu);
        helpMenu.add(new MenuItem("About"));
        
        mb.add(fileMenu);
        mb.add(editMenu);
        mb.add(helpMenu);
        
        setMenuBar(mb);
        
        // Menu item action
        exitItem.addActionListener(e -> System.exit(0));
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new MenuBarDemo();
    }
}
```

---

## PART C: APPLETS

---

## 12. Applets Basics

### 12.1 What is an Applet?

An **Applet** is a small Java program that runs inside a **web browser** or applet viewer. It extends `java.applet.Applet` class.

> **Note:** Applets are deprecated in modern Java (removed in Java 11+), but still asked in exams.

### 12.2 Applet vs Application

| Feature | Applet | Application |
|---------|--------|-------------|
| **Execution** | Inside browser | Standalone |
| **main() method** | Not needed | Required |
| **Security** | Runs in sandbox (restricted) | Full access |
| **File access** | Restricted | Allowed |
| **Network** | Only to host server | Any server |
| **Entry point** | init() method | main() method |

### 12.3 Applet Architecture

```
Browser/Applet Viewer
┌─────────────────────────────────┐
│         HTML Page               │
│  ┌───────────────────────────┐  │
│  │        Applet Area        │  │
│  │  ┌───────────────────┐    │  │
│  │  │  Java Applet      │    │  │
│  │  │  (runs in JVM)    │    │  │
│  │  └───────────────────┘    │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

### 12.4 Applet Life Cycle (Exam Important ⭐)

```
Browser loads HTML page
         │
         ↓
    ┌──────────┐
    │  init()  │  Called ONCE when applet is first loaded
    └────┬─────┘  (Initialization: set size, load images)
         ↓
    ┌──────────┐
    │  start() │  Called after init() and each time applet
    └────┬─────┘  becomes visible (brought back to view)
         ↓
    ┌──────────┐
    │  paint() │  Called to draw/render the applet
    └────┬─────┘  (Called by start() and repaint())
         ↓
    ┌──────────┐
    │  stop()  │  Called when applet goes out of view
    └────┬─────┘  (User switches tab/page)
         ↓
    ┌───────────┐
    │ destroy() │  Called ONCE when applet is unloaded
    └───────────┘  (Browser closes / page navigated away)
```

### 12.5 Applet Skeleton

```java
import java.applet.Applet;
import java.awt.Graphics;

public class MyApplet extends Applet {
    String message;
    
    // Called once when applet loads
    @Override
    public void init() {
        message = "Hello from Applet!";
        setBackground(java.awt.Color.YELLOW);
    }
    
    // Called each time applet becomes visible
    @Override
    public void start() {
        // Start animations, threads, etc.
    }
    
    // Called to draw/repaint the applet
    @Override
    public void paint(Graphics g) {
        g.drawString(message, 50, 50);
        g.drawRect(20, 20, 200, 100);
        g.drawOval(250, 20, 100, 100);
    }
    
    // Called when applet goes out of view
    @Override
    public void stop() {
        // Stop animations, threads, etc.
    }
    
    // Called once when applet is unloaded
    @Override
    public void destroy() {
        // Cleanup resources
    }
}
```

### 12.6 The HTML APPLET Tag

```html
<html>
<head><title>Applet Demo</title></head>
<body>
    <h1>My Java Applet</h1>
    
    <applet code="MyApplet.class" 
            width="400" 
            height="300"
            codebase="."
            alt="Applet not supported">
        
        <!-- Parameters -->
        <param name="message" value="Hello World">
        <param name="color" value="red">
        
        Your browser does not support Java Applets.
    </applet>
</body>
</html>
```

| Attribute | Description |
|-----------|-------------|
| `code` | Name of the applet class file |
| `width` | Width of the applet area |
| `height` | Height of the applet area |
| `codebase` | Base URL for the class file |
| `alt` | Alternative text |
| `align` | Alignment (left, right, center) |

### 12.7 Passing Parameters to Applets

```java
import java.applet.Applet;
import java.awt.*;

public class ParameterApplet extends Applet {
    String name;
    int fontSize;
    
    @Override
    public void init() {
        // Retrieve parameters from HTML
        name = getParameter("name");
        if (name == null) name = "Default";
        
        String sizeStr = getParameter("fontSize");
        fontSize = (sizeStr != null) ? Integer.parseInt(sizeStr) : 16;
    }
    
    @Override
    public void paint(Graphics g) {
        g.setFont(new Font("Arial", Font.BOLD, fontSize));
        g.drawString("Hello, " + name + "!", 50, 50);
    }
}
```

```html
<applet code="ParameterApplet.class" width="300" height="200">
    <param name="name" value="Rahul">
    <param name="fontSize" value="24">
</applet>
```

### 12.8 AppletContext and showDocument()

```java
import java.applet.*;
import java.awt.*;
import java.awt.event.*;
import java.net.*;

public class AppletContextDemo extends Applet {
    @Override
    public void init() {
        Button btn = new Button("Go to Google");
        add(btn);
        
        btn.addActionListener(e -> {
            try {
                AppletContext context = getAppletContext();
                URL url = new URL("https://www.google.com");
                
                // Open in same window
                context.showDocument(url);
                
                // Open in new window
                // context.showDocument(url, "_blank");
                
            } catch (MalformedURLException ex) {
                showStatus("Invalid URL");
            }
        });
    }
}
```

| Target | Description |
|--------|-------------|
| `"_self"` | Show in current frame |
| `"_parent"` | Show in parent frame |
| `"_top"` | Show in top-level frame |
| `"_blank"` | Show in new window |

---

## PART D: EVENT HANDLING

---

## 13. Delegation Event Model (Exam Important ⭐)

### 13.1 Concept

In the **Delegation Event Model**, event handling is delegated from the **source** (component that generates the event) to the **listener** (object that handles the event).

```
┌──────────┐     Event      ┌──────────────┐
│  Source   │ ──────────────→│   Listener   │
│ (Button) │   generates    │ (Handler)    │
│          │                │              │
│          │←── registers ──│ implements   │
│          │   listener     │ EventListener│
└──────────┘                └──────────────┘
```

### 13.2 Three Components

| Component | Description | Example |
|-----------|-------------|---------|
| **Event Source** | Component that generates the event | Button, TextField, Frame |
| **Event Object** | Object containing event information | ActionEvent, MouseEvent |
| **Event Listener** | Interface that handles the event | ActionListener, MouseListener |

### 13.3 Steps for Event Handling

```
Step 1: Create the source component (e.g., Button)
Step 2: Create a listener class implementing the listener interface
Step 3: Register the listener with the source
Step 4: Override the handler method(s)
```

---

## 14. Event Classes

### 14.1 Event Class Hierarchy

```
        ┌──────────────┐
        │ EventObject  │
        └──────┬───────┘
               ↓
        ┌──────────────┐
        │   AWTEvent   │
        └──────┬───────┘
    ┌──────┬───┼───┬──────┬──────────┐
    ↓      ↓   ↓   ↓      ↓          ↓
Action  Mouse Key  Window  Item    Text
Event   Event Event Event  Event   Event
         │
    ┌────┴────┐
MouseEvent  MouseWheelEvent
```

### 14.2 Common Event Classes

| Event Class | When Generated | Source Components |
|-------------|---------------|-------------------|
| `ActionEvent` | Button click, Enter in TextField | Button, TextField, MenuItem |
| `MouseEvent` | Mouse click, press, release, move | Any Component |
| `KeyEvent` | Key press, release, typed | Any Component |
| `WindowEvent` | Window open, close, resize | Window, Frame |
| `ItemEvent` | Checkbox, Choice selection | Checkbox, Choice, List |
| `TextEvent` | Text content changed | TextField, TextArea |
| `FocusEvent` | Component gains/loses focus | Any Component |
| `AdjustmentEvent` | Scrollbar adjusted | Scrollbar |

---

## 15. Event Listener Interfaces

| Listener Interface | Methods | For Event |
|-------------------|---------|-----------|
| `ActionListener` | `actionPerformed(ActionEvent)` | Button clicks |
| `MouseListener` | `mouseClicked()`, `mousePressed()`, `mouseReleased()`, `mouseEntered()`, `mouseExited()` | Mouse actions |
| `MouseMotionListener` | `mouseMoved()`, `mouseDragged()` | Mouse movement |
| `KeyListener` | `keyPressed()`, `keyReleased()`, `keyTyped()` | Keyboard |
| `WindowListener` | `windowOpened()`, `windowClosing()`, `windowClosed()`, `windowActivated()`, `windowDeactivated()`, `windowIconified()`, `windowDeiconified()` | Window events |
| `ItemListener` | `itemStateChanged(ItemEvent)` | Selection change |
| `TextListener` | `textValueChanged(TextEvent)` | Text change |

### 15.1 Example — ActionListener

```java
import java.awt.*;
import java.awt.event.*;

public class ActionListenerDemo extends Frame implements ActionListener {
    TextField tf;
    Button btn;
    Label result;
    
    ActionListenerDemo() {
        setTitle("Event Demo");
        setSize(300, 200);
        setLayout(new FlowLayout());
        
        tf = new TextField(15);
        btn = new Button("Click Me");
        result = new Label("  ");
        
        // Register listener
        btn.addActionListener(this);  // 'this' object handles events
        
        add(tf);
        add(btn);
        add(result);
        
        setVisible(true);
    }
    
    // Event handler method
    @Override
    public void actionPerformed(ActionEvent e) {
        result.setText("Hello, " + tf.getText() + "!");
    }
    
    public static void main(String[] args) {
        new ActionListenerDemo();
    }
}
```

---

## 16. Adapter Classes

### 16.1 What are Adapter Classes?

**Adapter classes** provide **empty implementations** of all methods in a listener interface. You only override the methods you need.

### 16.2 Why Use Adapter Classes?

```java
// WITHOUT Adapter - Must implement ALL 7 methods
class MyListener implements WindowListener {
    public void windowOpened(WindowEvent e) {}      // Empty
    public void windowClosing(WindowEvent e) {      // Only this one matters!
        System.exit(0);
    }
    public void windowClosed(WindowEvent e) {}      // Empty
    public void windowActivated(WindowEvent e) {}   // Empty
    public void windowDeactivated(WindowEvent e) {} // Empty
    public void windowIconified(WindowEvent e) {}   // Empty
    public void windowDeiconified(WindowEvent e) {} // Empty
}

// WITH Adapter - Only override what you need
class MyListener extends WindowAdapter {
    public void windowClosing(WindowEvent e) {
        System.exit(0);  // Only implement this!
    }
}
```

### 16.3 Common Adapter Classes

| Adapter Class | Implements |
|---------------|------------|
| `WindowAdapter` | `WindowListener` |
| `MouseAdapter` | `MouseListener` |
| `MouseMotionAdapter` | `MouseMotionListener` |
| `KeyAdapter` | `KeyListener` |
| `FocusAdapter` | `FocusListener` |
| `ComponentAdapter` | `ComponentListener` |

---

## PART E: SWING

---

## 17. Introduction to Swing

### 17.1 AWT vs Swing

| Feature | AWT | Swing |
|---------|-----|-------|
| **Package** | `java.awt` | `javax.swing` |
| **Components** | Heavy-weight (OS dependent) | Light-weight (Java drawn) |
| **Look & Feel** | Platform dependent | Platform independent (pluggable) |
| **MVC** | No | Yes (Model-View-Controller) |
| **Components** | Button, Label, TextField | JButton, JLabel, JTextField |
| **Features** | Basic | Rich (icons, tooltips, borders) |
| **Performance** | Faster (native) | Slightly slower (more features) |

### 17.2 Swing Class Hierarchy

```
        ┌──────────────┐
        │  Component   │ (AWT)
        └──────┬───────┘
               ↓
        ┌──────────────┐
        │  Container   │ (AWT)
        └──────┬───────┘
               ↓
        ┌──────────────┐
        │  JComponent  │ (Swing - base for all Swing components)
        └──────┬───────┘
    ┌──────┬───┼───┬──────┬─────────┐
    ↓      ↓   ↓   ↓      ↓         ↓
JButton JLabel JText  JPanel JCombo  JTabbed
               Field         Box     Pane
```

---

## 18. Core Java API Package & Reflection

### 18.1 Core API Packages

| Package | Purpose |
|---------|---------|
| `java.lang` | Core classes (String, Math, Thread) |
| `java.util` | Collections, Date, Random |
| `java.io` | Input/Output |
| `java.net` | Networking |
| `java.awt` | GUI (AWT) |
| `javax.swing` | GUI (Swing) |
| `java.sql` | Database |
| `java.lang.reflect` | Reflection API |

### 18.2 Reflection

**Reflection** allows examining and modifying the structure and behavior of classes **at runtime**.

```java
import java.lang.reflect.*;

class Student {
    private String name;
    public int age;
    
    public Student() {}
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void display() {
        System.out.println(name + " - " + age);
    }
    
    private void secret() {
        System.out.println("Secret method!");
    }
}

public class ReflectionDemo {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("Student");
        
        // Get class name
        System.out.println("Class: " + clazz.getName());
        
        // Get all methods
        System.out.println("\nMethods:");
        for (Method m : clazz.getDeclaredMethods()) {
            System.out.println("  " + m.getName() + " - " + 
                             Modifier.toString(m.getModifiers()));
        }
        
        // Get all fields
        System.out.println("\nFields:");
        for (Field f : clazz.getDeclaredFields()) {
            System.out.println("  " + f.getName() + " : " + f.getType());
        }
        
        // Create object dynamically
        Constructor<?> constructor = clazz.getConstructor(String.class, int.class);
        Object obj = constructor.newInstance("Rahul", 20);
        
        // Invoke method
        Method display = clazz.getMethod("display");
        display.invoke(obj);
        
        // Access private method
        Method secret = clazz.getDeclaredMethod("secret");
        secret.setAccessible(true);
        secret.invoke(obj);
    }
}
```

---

## 19. Swing Components

### 19.1 Swing Applet (JApplet)

```java
import javax.swing.*;
import java.awt.*;

public class SwingApplet extends JApplet {
    @Override
    public void init() {
        getContentPane().setBackground(Color.WHITE);
        
        JLabel label = new JLabel("Swing Applet!", SwingConstants.CENTER);
        label.setFont(new Font("Arial", Font.BOLD, 24));
        
        JButton btn = new JButton("Click Me");
        btn.addActionListener(e -> 
            JOptionPane.showMessageDialog(this, "Button clicked!"));
        
        getContentPane().setLayout(new BorderLayout());
        getContentPane().add(label, BorderLayout.CENTER);
        getContentPane().add(btn, BorderLayout.SOUTH);
    }
}
```

### 19.2 Icons & Labels

```java
import javax.swing.*;
import java.awt.*;

public class IconLabelDemo extends JFrame {
    IconLabelDemo() {
        setTitle("Icons and Labels");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new FlowLayout());
        
        // Text Label
        JLabel textLabel = new JLabel("Hello Swing!");
        textLabel.setFont(new Font("Arial", Font.BOLD, 20));
        
        // Icon Label
        ImageIcon icon = new ImageIcon("icon.png");
        JLabel iconLabel = new JLabel("With Icon", icon, SwingConstants.CENTER);
        
        // Label with both icon and text
        JLabel bothLabel = new JLabel("Text + Icon");
        bothLabel.setIcon(icon);
        bothLabel.setHorizontalTextPosition(SwingConstants.RIGHT);
        bothLabel.setVerticalTextPosition(SwingConstants.CENTER);
        
        add(textLabel);
        add(iconLabel);
        add(bothLabel);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new IconLabelDemo();
    }
}
```

### 19.3 Text Fields

```java
import javax.swing.*;
import java.awt.*;

public class TextFieldDemo extends JFrame {
    TextFieldDemo() {
        setTitle("Text Field Demo");
        setSize(400, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new FlowLayout());
        
        JTextField nameField = new JTextField(20);
        nameField.setToolTipText("Enter your name");
        
        JPasswordField passField = new JPasswordField(20);
        passField.setToolTipText("Enter password");
        
        JButton btn = new JButton("Submit");
        JLabel result = new JLabel("  ");
        
        btn.addActionListener(e -> {
            String name = nameField.getText();
            String pass = new String(passField.getPassword());
            result.setText("Name: " + name + ", Password length: " + pass.length());
        });
        
        add(new JLabel("Name:"));
        add(nameField);
        add(new JLabel("Password:"));
        add(passField);
        add(btn);
        add(result);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new TextFieldDemo();
    }
}
```

### 19.4 Buttons (JButton, JToggleButton, JRadioButton, JCheckBox)

```java
import javax.swing.*;
import java.awt.*;

public class ButtonDemo extends JFrame {
    ButtonDemo() {
        setTitle("Button Types Demo");
        setSize(500, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new FlowLayout());
        
        // JButton
        JButton btn = new JButton("Click Me");
        btn.addActionListener(e -> JOptionPane.showMessageDialog(this, "Clicked!"));
        
        // JToggleButton
        JToggleButton toggleBtn = new JToggleButton("Toggle");
        toggleBtn.addActionListener(e -> {
            if (toggleBtn.isSelected())
                toggleBtn.setText("ON");
            else
                toggleBtn.setText("OFF");
        });
        
        // JRadioButton (grouped)
        JRadioButton radio1 = new JRadioButton("Male");
        JRadioButton radio2 = new JRadioButton("Female");
        ButtonGroup group = new ButtonGroup();
        group.add(radio1);
        group.add(radio2);
        
        // JCheckBox
        JCheckBox check1 = new JCheckBox("Java");
        JCheckBox check2 = new JCheckBox("Python");
        JCheckBox check3 = new JCheckBox("C++");
        
        add(btn);
        add(toggleBtn);
        add(new JLabel("Gender:"));
        add(radio1);
        add(radio2);
        add(new JLabel("Languages:"));
        add(check1);
        add(check2);
        add(check3);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new ButtonDemo();
    }
}
```

### 19.5 Combo Boxes (JComboBox)

```java
import javax.swing.*;
import java.awt.*;

public class ComboBoxDemo extends JFrame {
    ComboBoxDemo() {
        setTitle("ComboBox Demo");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new FlowLayout());
        
        String[] items = {"Java", "Python", "C++", "JavaScript", "Kotlin"};
        JComboBox<String> comboBox = new JComboBox<>(items);
        comboBox.setEditable(true);  // Allow typing custom value
        
        JLabel selected = new JLabel("Selected: ");
        
        comboBox.addActionListener(e -> {
            selected.setText("Selected: " + comboBox.getSelectedItem());
        });
        
        add(new JLabel("Choose Language:"));
        add(comboBox);
        add(selected);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new ComboBoxDemo();
    }
}
```

### 19.6 Tabbed Panes (JTabbedPane)

```java
import javax.swing.*;
import java.awt.*;

public class TabbedPaneDemo extends JFrame {
    TabbedPaneDemo() {
        setTitle("Tabbed Pane Demo");
        setSize(500, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        JTabbedPane tabbedPane = new JTabbedPane();
        
        // Tab 1: Personal Info
        JPanel personalPanel = new JPanel(new FlowLayout());
        personalPanel.add(new JLabel("Name:"));
        personalPanel.add(new JTextField(15));
        personalPanel.add(new JLabel("Age:"));
        personalPanel.add(new JTextField(5));
        tabbedPane.addTab("Personal", personalPanel);
        
        // Tab 2: Education
        JPanel eduPanel = new JPanel(new FlowLayout());
        eduPanel.add(new JLabel("College:"));
        eduPanel.add(new JTextField(15));
        eduPanel.add(new JLabel("Course:"));
        String[] courses = {"B.Tech", "BCA", "MCA", "M.Tech"};
        eduPanel.add(new JComboBox<>(courses));
        tabbedPane.addTab("Education", eduPanel);
        
        // Tab 3: Settings
        JPanel settingsPanel = new JPanel(new FlowLayout());
        settingsPanel.add(new JCheckBox("Dark Mode"));
        settingsPanel.add(new JCheckBox("Notifications"));
        settingsPanel.add(new JCheckBox("Auto-Save"));
        tabbedPane.addTab("Settings", settingsPanel);
        
        add(tabbedPane);
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new TabbedPaneDemo();
    }
}
```

### 19.7 Scroll Panes (JScrollPane)

```java
import javax.swing.*;
import java.awt.*;

public class ScrollPaneDemo extends JFrame {
    ScrollPaneDemo() {
        setTitle("Scroll Pane Demo");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // TextArea inside ScrollPane
        JTextArea textArea = new JTextArea(20, 30);
        textArea.setText("This is a long text...\n".repeat(50));
        
        JScrollPane scrollPane = new JScrollPane(textArea);
        scrollPane.setVerticalScrollBarPolicy(
            JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
        scrollPane.setHorizontalScrollBarPolicy(
            JScrollPane.HORIZONTAL_SCROLLBAR_AS_NEEDED);
        
        add(scrollPane);
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new ScrollPaneDemo();
    }
}
```

---

## 20. AWT: Handling Events by Extending AWT Components

```java
import java.awt.*;
import java.awt.event.*;

// Custom Button that handles its own events
class MyButton extends Button {
    MyButton(String label) {
        super(label);
        enableEvents(AWTEvent.ACTION_EVENT_MASK);
    }
    
    @Override
    protected void processActionEvent(ActionEvent e) {
        System.out.println("Button clicked: " + getLabel());
        super.processActionEvent(e);
    }
}

class MyTextField extends TextField {
    MyTextField(int columns) {
        super(columns);
        enableEvents(AWTEvent.KEY_EVENT_MASK);
    }
    
    @Override
    protected void processKeyEvent(KeyEvent e) {
        if (e.getID() == KeyEvent.KEY_TYPED) {
            // Only allow digits
            if (!Character.isDigit(e.getKeyChar())) {
                e.consume();  // Swallow the event
                return;
            }
        }
        super.processKeyEvent(e);
    }
}

public class ExtendingComponentsDemo extends Frame {
    ExtendingComponentsDemo() {
        setTitle("Extending Components");
        setSize(300, 200);
        setLayout(new FlowLayout());
        
        add(new MyButton("Custom Button"));
        add(new Label("Numbers only: "));
        add(new MyTextField(15));
        
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new ExtendingComponentsDemo();
    }
}
```

---

## 21. Working with Graphics in AWT

```java
import java.awt.*;
import java.awt.event.*;

public class GraphicsDemo extends Frame {
    GraphicsDemo() {
        setTitle("Graphics Demo");
        setSize(500, 400);
        setVisible(true);
    }
    
    @Override
    public void paint(Graphics g) {
        // Set color
        g.setColor(Color.RED);
        g.drawString("Hello Java Graphics!", 50, 80);
        
        // Rectangle
        g.setColor(Color.BLUE);
        g.drawRect(50, 100, 150, 80);       // Outline
        g.fillRect(220, 100, 150, 80);      // Filled
        
        // Oval
        g.setColor(Color.GREEN);
        g.drawOval(50, 200, 100, 80);       // Outline
        g.fillOval(170, 200, 100, 80);      // Filled
        
        // Line
        g.setColor(Color.BLACK);
        g.drawLine(50, 300, 400, 300);
        
        // Arc
        g.setColor(Color.ORANGE);
        g.drawArc(300, 200, 100, 100, 0, 180);
        
        // Polygon
        g.setColor(Color.MAGENTA);
        int[] xPoints = {350, 400, 450};
        int[] yPoints = {300, 250, 300};
        g.fillPolygon(xPoints, yPoints, 3);  // Triangle
    }
    
    public static void main(String[] args) {
        new GraphicsDemo();
    }
}
```

---

## 22. Creating a Frame Window in an Applet

```java
import java.applet.*;
import java.awt.*;
import java.awt.event.*;

public class FrameInApplet extends Applet {
    Frame myFrame;
    
    @Override
    public void init() {
        Button btn = new Button("Open Frame");
        add(btn);
        
        btn.addActionListener(e -> {
            myFrame = new Frame("Frame from Applet");
            myFrame.setSize(300, 200);
            myFrame.setLayout(new FlowLayout());
            myFrame.add(new Label("This is a Frame window!"));
            myFrame.add(new Button("Close"));
            
            myFrame.addWindowListener(new WindowAdapter() {
                public void windowClosing(WindowEvent we) {
                    myFrame.dispose();
                }
            });
            
            myFrame.setVisible(true);
        });
    }
    
    @Override
    public void paint(Graphics g) {
        g.drawString("Click button to open Frame", 10, 60);
    }
}
```

---

## 23. Input and Output Streams — Streams vs Readers/Writers

### 23.1 Comparison

```
Byte Streams (8-bit)          Character Streams (16-bit)
┌─────────────────┐           ┌─────────────────┐
│  InputStream    │           │    Reader        │
│  OutputStream   │           │    Writer        │
└─────────────────┘           └─────────────────┘
     │                              │
     ├── FileInputStream             ├── FileReader
     ├── FileOutputStream            ├── FileWriter
     ├── BufferedInputStream         ├── BufferedReader
     ├── BufferedOutputStream        ├── BufferedWriter
     ├── DataInputStream             ├── InputStreamReader
     ├── DataOutputStream            ├── OutputStreamWriter
     ├── ObjectInputStream           ├── PrintWriter
     └── ObjectOutputStream          └── StringReader/Writer
```

### 23.2 StreamTokenizer

Breaks input into **tokens** (words, numbers, end-of-line).

```java
import java.io.*;

public class StreamTokenizerDemo {
    public static void main(String[] args) throws IOException {
        String input = "Hello 42 World 3.14 Java";
        StreamTokenizer st = new StreamTokenizer(
            new StringReader(input));
        
        while (st.nextToken() != StreamTokenizer.TT_EOF) {
            switch (st.ttype) {
                case StreamTokenizer.TT_WORD:
                    System.out.println("Word: " + st.sval);
                    break;
                case StreamTokenizer.TT_NUMBER:
                    System.out.println("Number: " + st.nval);
                    break;
            }
        }
    }
}
/* Output:
   Word: Hello
   Number: 42.0
   Word: World
   Number: 3.14
   Word: Java
*/
```

### 23.3 Piped Input and Output

Used for **communication between threads**.

```java
import java.io.*;

public class PipedStreamDemo {
    public static void main(String[] args) throws Exception {
        PipedOutputStream pos = new PipedOutputStream();
        PipedInputStream pis = new PipedInputStream(pos);
        
        // Writer thread
        Thread writer = new Thread(() -> {
            try {
                String msg = "Hello through pipe!";
                pos.write(msg.getBytes());
                pos.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        });
        
        // Reader thread
        Thread reader = new Thread(() -> {
            try {
                int ch;
                while ((ch = pis.read()) != -1) {
                    System.out.print((char) ch);
                }
                pis.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        });
        
        writer.start();
        reader.start();
    }
}
// Output: Hello through pipe!
```

---

## 24. Trees (JTree)

### 24.1 What is JTree?

**JTree** is a Swing component that displays data in a **hierarchical tree structure** — similar to a file system or directory structure.

```
Tree Structure:
┌── Root
│   ├── Node 1
│   │   ├── Leaf 1.1
│   │   └── Leaf 1.2
│   ├── Node 2
│   │   ├── Leaf 2.1
│   │   └── Leaf 2.2
│   └── Node 3
│       └── Leaf 3.1
```

### 24.2 Key Classes

| Class | Description |
|-------|-------------|
| `JTree` | The tree component |
| `DefaultMutableTreeNode` | A node that can have children |
| `DefaultTreeModel` | Default data model |
| `TreePath` | Represents a path to a node |
| `TreeSelectionModel` | Handles selection |

### 24.3 Complete Example

```java
import javax.swing.*;
import javax.swing.tree.*;
import java.awt.*;

public class JTreeDemo extends JFrame {
    JTreeDemo() {
        setTitle("JTree Demo");
        setSize(400, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Create root node
        DefaultMutableTreeNode root = new DefaultMutableTreeNode("University");
        
        // Create branch nodes
        DefaultMutableTreeNode csDept = new DefaultMutableTreeNode("CS Department");
        DefaultMutableTreeNode ecDept = new DefaultMutableTreeNode("EC Department");
        DefaultMutableTreeNode meDept = new DefaultMutableTreeNode("ME Department");
        
        // Add branches to root
        root.add(csDept);
        root.add(ecDept);
        root.add(meDept);
        
        // Add leaf nodes
        csDept.add(new DefaultMutableTreeNode("Java Programming"));
        csDept.add(new DefaultMutableTreeNode("Data Structures"));
        csDept.add(new DefaultMutableTreeNode("DBMS"));
        
        ecDept.add(new DefaultMutableTreeNode("Digital Electronics"));
        ecDept.add(new DefaultMutableTreeNode("Signal Processing"));
        
        meDept.add(new DefaultMutableTreeNode("Thermodynamics"));
        meDept.add(new DefaultMutableTreeNode("Fluid Mechanics"));
        
        // Create JTree
        JTree tree = new JTree(root);
        
        // Add selection listener
        tree.addTreeSelectionListener(e -> {
            DefaultMutableTreeNode selectedNode = 
                (DefaultMutableTreeNode) tree.getLastSelectedPathComponent();
            if (selectedNode != null) {
                System.out.println("Selected: " + selectedNode.getUserObject());
            }
        });
        
        // Add to scroll pane
        JScrollPane scrollPane = new JScrollPane(tree);
        add(scrollPane);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new JTreeDemo();
    }
}
```

### 24.4 Tree Operations

```java
// Expand all nodes
for (int i = 0; i < tree.getRowCount(); i++) {
    tree.expandRow(i);
}

// Collapse all
tree.collapseRow(0);

// Get selected node
DefaultMutableTreeNode node = 
    (DefaultMutableTreeNode) tree.getLastSelectedPathComponent();

// Add a node dynamically
DefaultMutableTreeNode newNode = new DefaultMutableTreeNode("New Subject");
csDept.add(newNode);
((DefaultTreeModel) tree.getModel()).reload();  // Refresh

// Remove a node
csDept.remove(newNode);
((DefaultTreeModel) tree.getModel()).reload();
```

---

## 25. Tables (JTable) (Exam Important ⭐)

### 25.1 What is JTable?

**JTable** is a Swing component that displays data in a **two-dimensional grid** (rows and columns) — similar to a spreadsheet.

### 25.2 Complete Example

```java
import javax.swing.*;
import javax.swing.table.*;
import java.awt.*;

public class JTableDemo extends JFrame {
    JTableDemo() {
        setTitle("JTable Demo");
        setSize(600, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Column names
        String[] columns = {"Roll No", "Name", "Marks", "Grade"};
        
        // Row data
        Object[][] data = {
            {101, "Rahul Sharma", 92.5, "A+"},
            {102, "Priya Patel", 85.0, "A"},
            {103, "Amit Kumar", 78.0, "B+"},
            {104, "Neha Gupta", 95.0, "A+"},
            {105, "Vijay Singh", 65.5, "B"},
            {106, "Sneha Reddy", 88.0, "A"},
        };
        
        // Create JTable
        JTable table = new JTable(data, columns);
        
        // Customize appearance
        table.setRowHeight(25);
        table.setFont(new Font("Arial", Font.PLAIN, 14));
        table.getTableHeader().setFont(new Font("Arial", Font.BOLD, 14));
        table.setSelectionBackground(new Color(173, 216, 230));
        
        // Auto-resize columns
        table.setAutoResizeMode(JTable.AUTO_RESIZE_ALL_COLUMNS);
        
        // Add to scroll pane (required for header to show)
        JScrollPane scrollPane = new JScrollPane(table);
        
        // Selection listener
        table.getSelectionModel().addListSelectionListener(e -> {
            if (!e.getValueIsAdjusting()) {
                int row = table.getSelectedRow();
                if (row >= 0) {
                    System.out.println("Selected: " + table.getValueAt(row, 1));
                }
            }
        });
        
        add(scrollPane);
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new JTableDemo();
    }
}
```

### 25.3 Using DefaultTableModel (Editable Table)

```java
import javax.swing.*;
import javax.swing.table.*;
import java.awt.*;

public class EditableTableDemo extends JFrame {
    DefaultTableModel model;
    
    EditableTableDemo() {
        setTitle("Editable Table");
        setSize(500, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());
        
        String[] columns = {"ID", "Name", "Age"};
        model = new DefaultTableModel(columns, 0);
        
        // Add initial data
        model.addRow(new Object[]{1, "Alice", 20});
        model.addRow(new Object[]{2, "Bob", 22});
        
        JTable table = new JTable(model);
        add(new JScrollPane(table), BorderLayout.CENTER);
        
        // Buttons panel
        JPanel btnPanel = new JPanel();
        JButton addBtn = new JButton("Add Row");
        JButton deleteBtn = new JButton("Delete Row");
        
        addBtn.addActionListener(e -> {
            int id = model.getRowCount() + 1;
            model.addRow(new Object[]{id, "New", 18});
        });
        
        deleteBtn.addActionListener(e -> {
            int selectedRow = table.getSelectedRow();
            if (selectedRow >= 0) {
                model.removeRow(selectedRow);
            }
        });
        
        btnPanel.add(addBtn);
        btnPanel.add(deleteBtn);
        add(btnPanel, BorderLayout.SOUTH);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new EditableTableDemo();
    }
}
```

### 25.4 JTable Key Methods

| Method | Description |
|--------|-------------|
| `getValueAt(row, col)` | Get cell value |
| `setValueAt(val, row, col)` | Set cell value |
| `getSelectedRow()` | Get selected row index |
| `getRowCount()` | Get number of rows |
| `getColumnCount()` | Get number of columns |
| `addRow(Object[])` | Add a new row (DefaultTableModel) |
| `removeRow(int)` | Remove a row (DefaultTableModel) |

---

## PART F: EXPLORING JAVA LANGUAGE

---

## 26. Simple Type Wrappers (Exam Important ⭐)

### 26.1 What are Wrapper Classes?

**Wrapper classes** convert **primitive types** into **objects**. Each primitive type has a corresponding wrapper class in `java.lang`.

### 26.2 Primitive → Wrapper Mapping

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

### 26.3 Autoboxing and Unboxing

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

### 26.4 Useful Wrapper Methods

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

### 26.5 Why Wrapper Classes are Needed

1. **Collections** only work with objects, not primitives (`ArrayList<Integer>`)
2. **Null values** — primitives can't be null, but wrapper objects can
3. **Utility methods** — parseInt(), toString(), compareTo(), etc.
4. **Generics** require object types (`List<int>` ✗, `List<Integer>` ✓)
5. **Serialization** — objects can be serialized

---

## 27. Runtime Memory Management

### 27.1 Java Memory Areas

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

### 27.2 Memory Areas Explained

| Area | Stores | Lifetime |
|------|--------|----------|
| **Stack** | Local variables, method calls, references | Per thread; freed when method returns |
| **Heap** | Objects, instance variables | Shared; freed by Garbage Collector |
| **Method Area** | Class metadata, static variables, bytecode | Until class is unloaded |
| **String Pool** | String literals | Shared; part of heap |
| **PC Register** | Current instruction of each thread | Per thread |
| **Native Stack** | Native (C/C++) method calls | Per thread |

### 27.3 Garbage Collection (Exam Important ⭐)

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

### 27.4 Runtime Class

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

### 27.5 Key Points about GC

| Point | Description |
|-------|-------------|
| **Automatic** | JVM handles memory deallocation |
| **Non-deterministic** | Cannot predict exactly when GC will run |
| `System.gc()` | Only a **request**, not guaranteed |
| `finalize()` | Called before GC reclaims the object (deprecated in Java 9+) |
| **Eligibility** | Object with no live references is eligible |
| **GC Algorithms** | Serial, Parallel, CMS, G1, ZGC |

---

## 28. Object Cloning — clone() and Cloneable Interface (Exam Important ⭐)

### 28.1 What is Cloning?

**Cloning** creates an **exact copy** of an existing object. Java provides the `clone()` method (in `Object` class) and the `Cloneable` interface.

### 28.2 Steps to Clone an Object

```
Step 1: Implement the Cloneable interface (marker interface)
Step 2: Override the clone() method from Object class
Step 3: Call super.clone() inside clone()
Step 4: Handle CloneNotSupportedException
```

### 28.3 Shallow Clone

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

### 28.4 Deep Clone

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

### 28.5 Shallow vs Deep Clone

| Feature | Shallow Clone | Deep Clone |
|---------|---------------|------------|
| **Nested objects** | Shared references | New copies |
| **Speed** | Faster | Slower |
| **Complexity** | Simple | Complex |
| **Independence** | Changes affect both | Fully independent |
| **Default in Java** | Yes (`super.clone()`) | Must implement manually |

---

## 29. Thread, ThreadGroup, and Runnable

### 29.1 Thread Class — Key Methods

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

### 29.2 Runnable Interface

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

### 29.3 ThreadGroup (Exam Important ⭐)

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

### 29.4 ThreadGroup Key Methods

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

### 29.5 Daemon Threads

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

### 29.6 Thread vs Runnable — Complete Comparison

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

## 30. Important Exam Questions

### Short Answer Questions
1. What is polymorphism? List its varieties.
2. What is a polymorphic variable? Give an example.
3. Differentiate between AWT and Swing.
4. What is the Delegation Event Model? Explain with diagram.
5. What are Adapter classes? Why are they used?
6. Explain the Applet life cycle with diagram.
7. What is reflection in Java?
8. List 5 layout managers and describe each briefly.
9. What are wrapper classes? List all 8 wrapper classes.
10. What is the difference between shallow clone and deep clone?
11. What is a ThreadGroup? List its methods.
12. Differentiate between Thread class and Runnable interface.

### Long Answer Questions
1. Explain all varieties of polymorphism with Java code examples.
2. What are Applets? Explain the applet life cycle, HTML tag, and parameter passing.
3. Explain the AWT class hierarchy with diagram. Describe any 5 AWT components.
4. Explain Event Handling in Java with the Delegation Event Model, Event Classes, and Listener Interfaces.
5. Write a program using Swing components: JFrame, JButton, JTextField, JComboBox, JTabbedPane, JTree, and JTable.
6. Explain Streams vs Readers/Writers. Write a program demonstrating StreamTokenizer.
7. Write a program creating a Frame window with MenuBar, Panel, and event handling.
8. Explain object cloning in Java. Differentiate between shallow and deep cloning with code examples.
9. Explain Java Runtime Memory Management. What is Garbage Collection? How does it work?
10. What are Wrapper classes? Explain autoboxing and unboxing with examples.
11. Explain ThreadGroup with example. How are daemon threads different from user threads?

---

> **Exam Tip:** For AWT/Swing questions, always draw the **class hierarchy** and explain the **Delegation Event Model** with a diagram showing Source → Event Object → Listener. For cloning questions, always draw the **memory diagram** showing shared vs separate references.
