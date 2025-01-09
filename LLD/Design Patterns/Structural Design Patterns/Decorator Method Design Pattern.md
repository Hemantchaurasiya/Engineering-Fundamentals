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

