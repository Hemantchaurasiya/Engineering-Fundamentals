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

## **References**
- [Design Patterns: Elements of Reusable Object-Oriented Software](https://en.wikipedia.org/wiki/Design_Patterns)
- [Adapter Pattern - GeeksforGeeks](https://www.geeksforgeeks.org/adapter-pattern/)

---

