---
title: "Open-Closed Principle: SOLID principles"
written by: "Rohit Singh Bhandari"
date: 2023-05-31T16:40:22+05:30
draft: false
---

## Introduction:<br>
SOLID is a set of principles that guides software developers in designing robust and maintainable code. Among these principles, the Open-Closed Principle (OCP) stands out as a fundamental concept. In this blog post, we will dive into the Open-Closed Principle and explore how it can be applied in Java programming, along with practical examples.

## What is the Open-Closed Principle (OCP)?<br>
The Open-Closed Principle, coined by Bertrand Meyer, states that "software entities (classes, modules, functions, etc.) should be open for extension but closed for modification." In simpler terms, it suggests that once a class is implemented and deployed, it should not be modified to incorporate new functionality. Instead, the class should be designed in such a way that it can be extended without modifying its existing code.

**Example Scenario:**
Let's consider an online shopping application where we have different types of products. For simplicity, we will focus on two product types: Books and Electronics. Each product type has a unique behavior, such as calculating shipping costs differently. Initially, we implement two classes: Book and Electronic to represent these product types.

```java
    public class Book {
        private String title;
        private double price;

        // Constructor, getters, and setters

        public double calculateShippingCost() {
            // Logic for calculating shipping cost for books
            return price * 0.05;
        }
    }

    public class Electronic {
        private String name;
        private double price;

        // Constructor, getters, and setters

        public double calculateShippingCost() {
            // Logic for calculating shipping cost for electronics
            return price * 0.1;
        }
    }
```

**The Problem:**<br>
Our application is thriving, and new product types are being introduced regularly. This means we'll need to modify the existing classes every time a new product type is added. This violates the Open-Closed Principle because we are modifying the existing code instead of extending it.

**Applying the Open-Closed Principle:**<br>
To adhere to the Open-Closed Principle, we need to refactor our code. The goal is to allow new product types to be added without modifying the existing classes. We can achieve this by introducing an abstract class called Product that provides a common interface for all product types:

```java
    public abstract class Product {
        protected String name;
        protected double price;

        // Constructor, getters, and setters

        public abstract double calculateShippingCost();
    }
```

We make the Product class abstract and define the calculateShippingCost() method as an abstract method. Now, any new product type should inherit from the Product class & implement its own version of the calculateShippingCost() method.

_Let's create a new class called Furniture to demonstrate this extension:_

```java
    public class Furniture extends Product {
        private String material;

        // Constructor, getters, and setters

        @Override
        public double calculateShippingCost() {
            // Logic for calculating shipping cost for furniture
            return price * 0.2;
        }
    }
```

Now, with the Product class and its extension Furniture, we can introduce new product types by extending the Product class without modifying the existing code.

## Benefits and Conclusion:
By adhering to the Open-Closed Principle, we achieve code that is more flexible, reusable, and maintainable. When new requirements arise, we can easily introduce new functionality by extending existing classes instead of modifying them. This minimizes the risk of introducing bugs or breaking existing functionality.

Thank you!