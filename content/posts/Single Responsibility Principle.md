---
title: "Single Responsibility Principle: SOLID Principles"
date: 2023-05-30T15:07:22+05:30
draft: false
---

# Understanding the Single Responsibility Principle 

## Introduction:<br>
In development, it's crucial to learn about software design principles that can help you write clean, maintainable, and scalable code. One such principle is the Single Responsibility Principle (SRP). In this blog post, we will explore what SRP is, why it's important, and provide an example in Java to help solidify understanding.

### What is the Single Responsibility Principle?<br>
The Single Responsibility Principle states that a class should have only one reason to change. In other words, a class should have a single responsibility or concern. By keeping classes focused on a single task, we improve code readability, maintainability, and reusability.

**Example:**<br>
Let's say we're developing a simple online shopping application, and we have a class called Order that represents an order placed by a customer. The Order class may have multiple responsibilities, such as calculating the total cost, applying discounts, and generating an invoice. However, applying SRP, we would separate these responsibilities into different classes.

``` java
    public class Order {
        private List<OrderItem> items;
        private Customer customer;
        // other order-related attributes
        
        // Constructor, getters, setters, and other methods
        
        public double calculateTotalCost() {
            double totalCost = 0;
            for (OrderItem item : items) {
                totalCost += item.getPrice() * item.getQuantity();
            }
            return totalCost;
        }
        
        public void applyDiscount(double discountPercentage) {
            // Applying discount logic
        }
        
        public void generateInvoice() {
            // Generating invoice logic
        }
    }
```

In the above code snippet, the Order class violates the SRP because it has multiple responsibilities. Let's refactor it to adhere to the SRP:

``` java
    public class Order {
        private List<OrderItem> items;
        private Customer customer;
        // other order-related attributes
        
        // Constructor, getters, setters, and other methods
        
        public double calculateTotalCost() {
            double totalCost = 0;
            for (OrderItem item : items) {
                totalCost += item.getPrice() * item.getQuantity();
            }
            return totalCost;
        }
    }

    public class Discount {
        public void applyDiscount(Order order, double discountPercentage) {
            // Applying discount logic
        }
    }

    public class InvoiceGenerator {
        public void generateInvoice(Order order) {
            // Generating invoice logic
        }
    }
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;By separating the responsibilities into different classes, we now have a more maintainable and extensible codebase. The Order class is responsible for managing order-related information, the Discount class handles applying discounts, and the InvoiceGenerator class focuses solely on generating invoices.

### Benefits of the Single Responsibility Principle:<br>
Adhering to the Single Responsibility Principle offers several advantages:

1. Improved code readability: Each class has a clear and focused purpose, making it easier for developers to understand and maintain the codebase.

2. Easier testing: Classes with single responsibilities are easier to test since they have fewer dependencies and a clear scope of functionality.

3. Enhanced modularity: Code that follows SRP is more modular, allowing for easier reuse of individual components in other parts of the system.

4. Reduced impact of changes: When a single responsibility changes, only the class responsible for that concern needs to be modified. This minimizes the potential ripple effects throughout the codebase.

### Conclusion:
The Single Responsibility Principle is a crucial concept to grasp for beginners in Java development. By ensuring that each class has a single responsibility, we can build more maintainable and scalable software systems. By applying SRP, you'll be on your way to writing cleaner, more organized code that is easier.
Now our class structure obeys the Single Responsibility Principle and every class is responsible for one aspect of our application. Great!

