---
title: "Liskov Substitution Principle: SOLID principles"
written by: "Rohit Singh Bhandari"
date: 2023-06-01T15:58:22+05:30
draft: false
---

## Introduction:<br>
One such principle that plays a crucial role in object-oriented programming is the Liskov Substitution Principle (LSP). Coined by Barbara Liskov, this principle emphasizes the significance of substitutability and inheritance in building reliable and flexible software systems. In this blog, we'll explore the Liskov Substitution Principle and its practical implications.

## Understanding the Liskov Substitution Principle:<br>
At its core, the Liskov Substitution Principle (LSP) is a fundamental principle of object-oriented programming. It states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, if a piece of code works with a certain type, it should also work with any subtype of that type.

Let's illustrate the Liskov Substitution Principle with an example in Java. Consider a scenario where we have a base class called Shape that defines the common properties and behaviors of different shapes. We will create a subclass called Rectangle that inherits from Shape.

```java
    class Shape {
        protected int width;
        protected int height;

        public void setWidth(int width) {
            this.width = width;
        }

        public void setHeight(int height) {
            this.height = height;
        }

        public int getArea() {
            return width * height;
        }
    }

    class Rectangle extends Shape {
        public void setWidth(int width) {
            super.setWidth(width);
        }

        public void setHeight(int height) {
            super.setHeight(height);
        }
    }
``` 

In the above example, we have a Shape class with two properties, width and height, along with getters and setters. It also has a method getArea() that calculates the area of the shape.
&nbsp;&nbsp;&nbsp;&nbsp;Now, let's see how the Liskov Substitution Principle comes into play. According to the LSP, objects of a subclass should be able to replace objects of the superclass without altering the correctness of the program.

```java
    class AreaCalculator {
        public int calculateArea(Shape shape) {
            shape.setWidth(10);
            shape.setHeight(20);
            return shape.getArea();
        }
    }

    public class Main {
        public static void main(String[] args) {
            Shape shape = new Shape();
            Rectangle rectangle = new Rectangle();

            AreaCalculator calculator = new AreaCalculator();
            int shapeArea = calculator.calculateArea(shape);
            int rectangleArea = calculator.calculateArea(rectangle);

            System.out.println("Shape area: " + shapeArea);
            System.out.println("Rectangle area: " + rectangleArea);
        }
    }
```

In the above code, we have a class AreaCalculator that calculates the area of a shape. It takes an object of type Shape as a parameter and sets its width and height to calculate the area. In the main() method, we create an instance of Shape and Rectangle, and then pass them to the AreaCalculator to calculate their respective areas.

By adhering to the Liskov Substitution Principle, we can substitute the Shape object with a Rectangle object without affecting the correctness of the program. The Rectangle class extends the Shape class and inherits its properties and behaviors. It overrides the setWidth() and setHeight() methods to ensure they work correctly for a rectangle shape.

_The output of the above code will be:_

```java
    Shape area: 200
    Rectangle area: 200
```

&nbsp;&nbsp;&nbsp;&nbsp;As you can see, the calculateArea() method works correctly for both the Shape and Rectangle objects. The LSP allows us to treat the Rectangle object as a valid substitute for the Shape object, maintaining the expected behavior of the program.

## Conclusion:
The Liskov Substitution Principle is a crucial principle in object-oriented programming that ensures the substitutability and consistency of objects in an inheritance hierarchy. By adhering to this principle, you can create more maintainable and flexible software systems, promoting code reuse and modularity. Applying the LSP leads to robust and reliable code, as well as improved testability. By understanding and implementing the Liskov Substitution Principle effectively, you can enhance the quality and longevity of your software projects.