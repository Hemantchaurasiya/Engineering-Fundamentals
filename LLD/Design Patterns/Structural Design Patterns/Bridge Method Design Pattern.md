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

