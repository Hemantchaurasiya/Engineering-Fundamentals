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

