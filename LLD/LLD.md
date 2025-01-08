### Low level Design

# Adapter Design Pattern

## **Overview**
The **Adapter Pattern** is a structural design pattern that allows incompatible interfaces or classes to work together by acting as a bridge between them. It is commonly used to integrate third-party libraries or legacy systems into existing code without modifying their source.

---

## **When to Use the Adapter Pattern**
Use the Adapter Pattern when:
- You need to integrate a new component with an interface that does not match your existing system.
- You want to reuse existing code without altering its implementation.
- You need to integrate third-party libraries or legacy systems that are incompatible with your application's interface.

---

## **Why Use the Adapter Pattern?**
- **Interoperability:** Makes incompatible interfaces work together.
- **Code Reusability:** Allows the use of pre-existing libraries or classes without modifying them.
- **Integration Simplification:** Helps in seamless integration of external systems or libraries.

---

## **Advantages and Disadvantages**

### **Advantages:**
- Promotes reusability by enabling compatibility between different interfaces.
- Adheres to the **Open/Closed Principle** (open for extension, closed for modification).
- Simplifies system integration by decoupling client code from specific implementations.

### **Disadvantages:**
- Adds an extra layer of abstraction, increasing system complexity.
- Can lead to performance overhead due to indirection.
- May make the system harder to understand for new developers.

---

## **Analogy**
A simple analogy is a **power socket adapter**. For example:
- A U.S. plug (two flat pins) and a European socket (two round pins) are incompatible.
- The power adapter bridges the gap, allowing the U.S. plug to connect to the European socket, enabling power flow without altering the plug or socket.

---

## **Real-World Use Case**
A common use case is integrating a third-party payment gateway into an e-commerce platform. The payment gateway's API might not match the platform's interface, and an adapter can help translate the calls between them.

---

## **Code Example: Integrating a Third-Party Payment Gateway in Java**

### **Scenario:**
- The platform uses its own `PaymentProcessor` interface.
- The third-party payment gateway provides a `ThirdPartyPayment` class with a different interface.
- An adapter (`PaymentAdapter`) bridges the two.

```java
// Step 1: Define the target interface expected by the e-commerce platform
interface PaymentProcessor {
    void processPayment(double amount);
}

// Step 2: Existing third-party payment gateway with its own interface
class ThirdPartyPayment {
    public void makePayment(double amount) {
        System.out.println("Processing payment of $" + amount + " through Third Party Gateway.");
    }
}

// Step 3: Create the Adapter that implements the target interface
class PaymentAdapter implements PaymentProcessor {
    private ThirdPartyPayment thirdPartyPayment;

    public PaymentAdapter(ThirdPartyPayment thirdPartyPayment) {
        this.thirdPartyPayment = thirdPartyPayment;
    }

    @Override
    public void processPayment(double amount) {
        // Adapts the call to the third-party method
        thirdPartyPayment.makePayment(amount);
    }
}

// Step 4: Client code using the adapter
public class ECommercePlatform {
    public static void main(String[] args) {
        // Create an instance of the third-party payment gateway
        ThirdPartyPayment thirdPartyPayment = new ThirdPartyPayment();

        // Create an adapter to bridge the platform and the third-party gateway
        PaymentProcessor paymentProcessor = new PaymentAdapter(thirdPartyPayment);

        // Process payment using the adapter
        paymentProcessor.processPayment(100.00);
    }
}
```

---

## **Explanation**
1. **Target Interface (`PaymentProcessor`)**:
   Defines the method `processPayment` that the e-commerce platform expects.

2. **Adaptee (`ThirdPartyPayment`)**:
   Represents the third-party payment gateway with its own method (`makePayment`).

3. **Adapter (`PaymentAdapter`)**:
   Bridges the gap by converting the `processPayment` call to the `makePayment` method.

4. **Client Code (`ECommercePlatform`)**:
   Uses the adapter to process payments seamlessly without being aware of the third-party implementation details.

---

## **Key Points**
- The Adapter Pattern simplifies working with incompatible interfaces.
- It enables code reusability and promotes integration without modifying existing implementations.
- A common use case is integrating third-party systems or APIs into an existing codebase.

---

# Bridge Design Pattern in Java

## Overview
The Bridge Design Pattern is a structural pattern that decouples an abstraction from its implementation, allowing both to vary independently. This pattern is especially useful when dealing with systems that have multiple abstractions and implementations.

In this example, we demonstrate the Bridge Design Pattern by creating a GUI system where different types of buttons can be rendered using different rendering systems (e.g., Windows and Mac).

---

## Key Components

1. **Implementor**: Defines the interface for the implementation classes. In this example, the `Renderer` interface represents the rendering system.
   - `WindowsRenderer`: A concrete implementation for rendering on Windows.
   - `MacRenderer`: A concrete implementation for rendering on Mac.

2. **Abstraction**: Defines the interface for the abstraction and maintains a reference to the implementor.
   - `Button`: An abstract class that delegates rendering to the `Renderer`.

3. **Refined Abstraction**: Extends the abstraction and provides additional behavior or specific details.
   - `ConcreteButton`: A specific implementation of the `Button` class with a label.

4. **Client**: Uses the abstraction to interact with the implementation. The client code remains decoupled from the implementation details.

---

## Class Diagram
```
Abstraction (Button)                  Implementor (Renderer)
       |                                    |
       |-------- Refined Abstraction        |------- Concrete Implementors
       |         (ConcreteButton)           |        (WindowsRenderer, MacRenderer)
       |                                    |
    Client                                 Implementation
```

---

## Code Example
### Step 1: Define the Implementor
```java
interface Renderer {
    void renderButton(String label);
}

class WindowsRenderer implements Renderer {
    @Override
    public void renderButton(String label) {
        System.out.println("Rendering button on Windows: " + label);
    }
}

class MacRenderer implements Renderer {
    @Override
    public void renderButton(String label) {
        System.out.println("Rendering button on Mac: " + label);
    }
}
```

### Step 2: Define the Abstraction
```java
abstract class Button {
    protected Renderer renderer;

    public Button(Renderer renderer) {
        this.renderer = renderer;
    }

    public abstract void draw();
}
```

### Step 3: Define the Refined Abstraction
```java
class ConcreteButton extends Button {
    private String label;

    public ConcreteButton(Renderer renderer, String label) {
        super(renderer);
        this.label = label;
    }

    @Override
    public void draw() {
        renderer.renderButton(label);
    }
}
```

### Step 4: Implement the Client
```java
public class BridgePatternExample {
    public static void main(String[] args) {
        Renderer windowsRenderer = new WindowsRenderer();
        Renderer macRenderer = new MacRenderer();

        Button button1 = new ConcreteButton(windowsRenderer, "OK");
        Button button2 = new ConcreteButton(macRenderer, "Cancel");

        button1.draw();  // Outputs: Rendering button on Windows: OK
        button2.draw();  // Outputs: Rendering button on Mac: Cancel
    }
}
```

---

## How It Works
1. **Client Code**: The client interacts with the `Button` abstraction without worrying about the underlying rendering system.
2. **Decoupling**: The `Renderer` implementation can be changed or extended without modifying the `Button` abstraction.
3. **Extensibility**: New rendering systems or button types can be added without impacting existing code.

---

## Advantages
- Promotes loose coupling between abstraction and implementation.
- Supports independent extension of abstractions and implementations.
- Reduces the risk of a "class explosion" by avoiding multiple subclasses for every combination of abstraction and implementation.

## Disadvantages
- Adds complexity due to the separation of abstraction and implementation.
- May not be suitable for small or simple systems.

---

## Real-World Use Cases
- **Cross-platform GUIs**: Decoupling GUI controls (buttons, sliders) from their rendering implementations (e.g., different operating systems).
- **File System Handling**: Abstracting file operations while having different implementations for local and remote file systems.

---

## How to Run
1. Copy the code into a Java IDE (e.g., IntelliJ IDEA, Eclipse).
2. Compile and run the `BridgePatternExample` class.
3. Observe the output:
   - Rendering button on Windows: OK
   - Rendering button on Mac: Cancel

---

## Conclusion
The Bridge Design Pattern is a powerful tool for decoupling abstraction and implementation, making the codebase more flexible and maintainable. This example demonstrates how you can use it in a GUI system, but it can be applied to many other real-world scenarios where decoupling is beneficial.




# Builder Design Pattern in Java

## Overview
The Builder Pattern is a creational design pattern used to construct complex objects step by step. It separates the construction process of an object from its representation, allowing the same construction process to create different representations. This pattern is particularly useful for creating objects with many optional parameters.

---

## Features of the Builder Pattern
- Simplifies the construction of complex objects.
- Ensures immutability of objects.
- Follows the **Single Responsibility Principle** by separating object construction from the object itself.
- Provides flexibility to reuse the same construction process for different representations.

---

## Real-World Analogy
Imagine building a custom sandwich at a restaurant. You specify the type of bread, protein, vegetables, and sauces. The builder (the person making the sandwich) follows your instructions step by step to construct the sandwich according to your preferences.

---

## Use Cases
- When a class has many optional fields or configurations.
- When the construction process involves several steps.
- To ensure immutability of the object being created.
- To construct objects with multiple representations or configurations.

---

## Real-World Example: Building a House
Below is an example implementation of the Builder Pattern in Java to construct a `House` object.

### Code Implementation

#### **House Class (Product)**
```java
public class House {
    private String foundation;
    private String structure;
    private String roof;
    private boolean hasGarden;
    private boolean hasSwimmingPool;

    // Private constructor to enforce immutability
    private House(HouseBuilder builder) {
        this.foundation = builder.foundation;
        this.structure = builder.structure;
        this.roof = builder.roof;
        this.hasGarden = builder.hasGarden;
        this.hasSwimmingPool = builder.hasSwimmingPool;
    }

    // Static Builder Class
    public static class HouseBuilder {
        private String foundation;
        private String structure;
        private String roof;
        private boolean hasGarden;
        private boolean hasSwimmingPool;

        public HouseBuilder setFoundation(String foundation) {
            this.foundation = foundation;
            return this;
        }

        public HouseBuilder setStructure(String structure) {
            this.structure = structure;
            return this;
        }

        public HouseBuilder setRoof(String roof) {
            this.roof = roof;
            return this;
        }

        public HouseBuilder setGarden(boolean hasGarden) {
            this.hasGarden = hasGarden;
            return this;
        }

        public HouseBuilder setSwimmingPool(boolean hasSwimmingPool) {
            this.hasSwimmingPool = hasSwimmingPool;
            return this;
        }

        public House build() {
            return new House(this);
        }
    }

    @Override
    public String toString() {
        return "House [foundation=" + foundation + ", structure=" + structure +
               ", roof=" + roof + ", hasGarden=" + hasGarden +
               ", hasSwimmingPool=" + hasSwimmingPool + "]";
    }
}
```

#### **Main Class**
```java
public class Main {
    public static void main(String[] args) {
        House house = new House.HouseBuilder()
                            .setFoundation("Concrete")
                            .setStructure("Wood and Brick")
                            .setRoof("Tiles")
                            .setGarden(true)
                            .setSwimmingPool(false)
                            .build();

        System.out.println(house);
    }
}
```

### Output
```
House [foundation=Concrete, structure=Wood and Brick, roof=Tiles, hasGarden=true, hasSwimmingPool=false]
```

---

## Advantages
1. **Readability:** Simplifies object creation with clear and readable code.
2. **Immutability:** Ensures that the created object is immutable.
3. **Reusability:** Allows the same process to create different representations of an object.
4. **Single Responsibility Principle:** Separates the logic of building an object from the object itself.

## Disadvantages
1. **Complexity:** Introduces additional builder classes, which may increase complexity for simpler objects.
2. **Overhead:** May be overkill for objects with only a few parameters.

---

## When to Use the Builder Pattern?
- When dealing with objects that have numerous optional parameters.
- When the construction process is complex or needs to be controlled step by step.
- When you want to ensure immutability of the objects being created.

---

## Related Design Patterns
- **Factory Pattern:** Focuses on creating objects without exposing the instantiation logic but is less flexible than the Builder pattern for constructing complex objects.
- **Prototype Pattern:** Focuses on cloning objects instead of building them step by step.

---

## Summary
The Builder Pattern is a powerful design pattern for constructing complex objects in a flexible and controlled way. By separating the construction process from the object itself, it ensures clarity, maintainability, and reusability in your code. Use it when your objects have many optional parameters or when the construction process requires multiple steps.


----------------------------------------------------------------------------------------------------------------


# Composite Method Pattern - File System Example

## Overview
The **Composite Method pattern** is a structural design pattern that allows you to compose objects into tree-like structures to represent part-whole hierarchies. It enables treating individual objects and compositions of objects uniformly.

This example demonstrates the Composite Method pattern applied to a file system, where both files and directories are treated as components of a hierarchical structure.

---

## Use Case: File System
The example implements a file system where:
- **File**: Represents individual files (leaf nodes).
- **Directory**: Represents directories that can contain files or other directories (composite nodes).

Both files and directories share a common interface, enabling operations like:
- Displaying details of all components.
- Calculating the total size of files and directories.

---

## Structure
### Classes and Interfaces:
1. **`FileSystemComponent`** (Interface):
   - Represents the common interface for both files and directories.
   - Methods:
     - `void showDetails()`: Displays details of the component.
     - `long getSize()`: Returns the size of the component.

2. **`File`** (Leaf):
   - Implements the `FileSystemComponent` interface.
   - Represents individual files.
   - Attributes:
     - `name`: Name of the file.
     - `size`: Size of the file.

3. **`Directory`** (Composite):
   - Implements the `FileSystemComponent` interface.
   - Represents directories that can contain files or other directories.
   - Attributes:
     - `name`: Name of the directory.
     - `components`: A list of `FileSystemComponent` (files and directories).

4. **`Main`** (Client):
   - Creates files and directories.
   - Adds files and directories to the tree structure.
   - Performs operations like displaying details and calculating total size.

---

## Code Example
Here is the implementation in Java:

```java
// Component
interface FileSystemComponent {
    void showDetails();
    long getSize();
}

// Leaf
class File implements FileSystemComponent {
    private String name;
    private long size;

    public File(String name, long size) {
        this.name = name;
        this.size = size;
    }

    @Override
    public void showDetails() {
        System.out.println("File: " + name + ", Size: " + size + " KB");
    }

    @Override
    public long getSize() {
        return size;
    }
}

// Composite
class Directory implements FileSystemComponent {
    private String name;
    private List<FileSystemComponent> components = new ArrayList<>();

    public Directory(String name) {
        this.name = name;
    }

    public void addComponent(FileSystemComponent component) {
        components.add(component);
    }

    @Override
    public void showDetails() {
        System.out.println("Directory: " + name);
        for (FileSystemComponent component : components) {
            component.showDetails();
        }
    }

    @Override
    public long getSize() {
        long totalSize = 0;
        for (FileSystemComponent component : components) {
            totalSize += component.getSize();
        }
        return totalSize;
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        FileSystemComponent file1 = new File("file1.txt", 120);
        FileSystemComponent file2 = new File("file2.txt", 200);

        FileSystemComponent directory1 = new Directory("Documents");
        ((Directory) directory1).addComponent(file1);
        ((Directory) directory1).addComponent(file2);

        FileSystemComponent file3 = new File("file3.txt", 150);
        FileSystemComponent directory2 = new Directory("Images");
        ((Directory) directory2).addComponent(file3);

        FileSystemComponent rootDirectory = new Directory("Root");
        ((Directory) rootDirectory).addComponent(directory1);
        ((Directory) rootDirectory).addComponent(directory2);

        // Show details of the entire file system
        rootDirectory.showDetails();

        // Get total size of all components in the root directory
        System.out.println("Total Size: " + rootDirectory.getSize() + " KB");
    }
}
```

---

## Output
When running the above code, the output will look like this:

```
Directory: Root
Directory: Documents
File: file1.txt, Size: 120 KB
File: file2.txt, Size: 200 KB
Directory: Images
File: file3.txt, Size: 150 KB
Total Size: 470 KB
```

---

## Pros and Cons of the Composite Method Pattern

### Pros:
1. **Simplifies client code**: Treats individual objects and composites uniformly.
2. **Flexible**: Allows for the dynamic addition of components.
3. **Easier maintenance**: Modifications to the structure are straightforward.

### Cons:
1. **Complexity**: Can become overly complicated for simple hierarchies.
2. **Operations**: Some operations might be hard to implement uniformly across components.

---

## Real-World Analogy
The Composite Method pattern is analogous to a **folder system on a computer**:
- Files are individual objects (leaf nodes).
- Folders are composite objects that can contain files or other folders.
- Both files and folders support operations like opening or deleting.

---

## Use Cases
1. **File systems**: Managing files and folders.
2. **Organizational structures**: Employees and teams.
3. **UI components**: Buttons, panels, and composite views.

---

## Conclusion
The Composite Method pattern is ideal for managing part-whole hierarchies where individual objects and groups of objects need to be treated in a uniform way. This file system example showcases its application and demonstrates how it simplifies working with hierarchical structures in Java.

--------------------------------------------------------------------------------------------------------------------------------

# Decorator Method Pattern in Java

## Introduction
The **Decorator Method pattern** is a structural design pattern that allows you to dynamically add functionality to objects at runtime. It provides a flexible alternative to subclassing for extending behavior, making it ideal for situations where behaviors need to be dynamically mixed and matched.

This repository contains an example implementation of the Decorator Method pattern using Java. The example focuses on enhancing a basic graphical shape (a circle) with additional features such as borders and colors.

---

## Key Concepts
### What is the Decorator Method Pattern?
The Decorator Method pattern dynamically adds new functionality to an object without altering its structure. It achieves this by using wrapper classes (decorators) that extend the behavior of the base component.

### Where to Use It
- When you want to add behavior dynamically at runtime.
- When subclassing is impractical due to a large number of combinations of behaviors.
- When enhancing an object’s functionality without modifying its code.

### Why Use It?
- To avoid subclass explosion.
- To keep the code flexible and maintainable.
- To adhere to the **Open/Closed Principle**, where objects are open for extension but closed for modification.

---

## Example Structure
The example in this repository includes:

### Components:
1. **`Shape` (Interface):** Defines the base functionality (drawing a shape).
2. **`Circle` (Concrete Component):** Implements the base functionality (drawing a circle).

### Decorators:
1. **`ShapeDecorator` (Abstract Decorator):** Wraps the `Shape` object and provides a base for additional functionality.
2. **`BorderDecorator` (Concrete Decorator):** Adds border functionality.
3. **`ColorDecorator` (Concrete Decorator):** Adds color functionality.

---

## Code Walkthrough
Below is the class diagram for the pattern:
```
Shape (Interface)
   ├── Circle (Concrete Component)
   ├── ShapeDecorator (Abstract Decorator)
         ├── BorderDecorator (Concrete Decorator)
         └── ColorDecorator (Concrete Decorator)
```

### Code Example

#### Interface and Concrete Component
```java
// Component interface
interface Shape {
    void draw();
}

// Concrete component
class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}
```

#### Abstract Decorator
```java
// Abstract decorator
abstract class ShapeDecorator implements Shape {
    protected Shape decoratedShape;

    public ShapeDecorator(Shape shape) {
        this.decoratedShape = shape;
    }

    @Override
    public void draw() {
        decoratedShape.draw();
    }
}
```

#### Concrete Decorators
```java
// Concrete decorator for adding borders
class BorderDecorator extends ShapeDecorator {
    public BorderDecorator(Shape shape) {
        super(shape);
    }

    @Override
    public void draw() {
        decoratedShape.draw();
        addBorder();
    }

    private void addBorder() {
        System.out.println("Adding Border");
    }
}

// Concrete decorator for adding color
class ColorDecorator extends ShapeDecorator {
    public ColorDecorator(Shape shape) {
        super(shape);
    }

    @Override
    public void draw() {
        decoratedShape.draw();
        addColor();
    }

    private void addColor() {
        System.out.println("Adding Color");
    }
}
```

#### Main Class
```java
public class DecoratorPatternExample {
    public static void main(String[] args) {
        Shape circle = new Circle();
        Shape redCircle = new ColorDecorator(new Circle());
        Shape borderedCircle = new BorderDecorator(new Circle());
        Shape redBorderedCircle = new BorderDecorator(new ColorDecorator(new Circle()));

        System.out.println("Simple Circle:");
        circle.draw();

        System.out.println("\nCircle with Red Color:");
        redCircle.draw();

        System.out.println("\nCircle with Border:");
        borderedCircle.draw();

        System.out.println("\nCircle with Red Color and Border:");
        redBorderedCircle.draw();
    }
}
```

---

## Output
```
Simple Circle:
Drawing a Circle

Circle with Red Color:
Drawing a Circle
Adding Color

Circle with Border:
Drawing a Circle
Adding Border

Circle with Red Color and Border:
Drawing a Circle
Adding Color
Adding Border
```

---

## Pros and Cons
### Pros:
1. Flexible and reusable.
2. Avoids subclass explosion.
3. Adheres to the Open/Closed Principle.

### Cons:
1. Can make the code complex with too many decorators.
2. Adds runtime overhead with multiple method calls.

---

## Real-World Analogy
Imagine you buy a basic coffee (base component). You can dynamically add milk, sugar, or whipped cream (decorators) to customize your coffee without altering the original coffee recipe.

---

## How to Run
1. Clone this repository.
2. Compile the Java files using a Java compiler:
   ```bash
   javac *.java
   ```
3. Run the `DecoratorPatternExample` class:
   ```bash
   java DecoratorPatternExample
   ```

---

## License
This project is licensed under the MIT License.

---

## Contributions
Feel free to fork the repository and submit pull requests for improvements or new examples of the Decorator Method pattern!

-------------------------------------------------------------------------------------------------------------------------------
