---
title: "Spring: DI Container"
date: 2023-04-02T23:14:22+05:30
draft: false
---

The Spring Framework is a popular and widely-used open-source framework for building Java-based       applications. It provides a comprehensive programming and configuration model for modern Java-based enterprise applications, including support for dependency injection, aspect-oriented programming, transaction management, and much more. Spring is designed to simplify the development process and improve the maintainability and scalability of applications. In this article, we will explore the key features of the Spring Framework and how it can be used to build robust, scalable applications.

The Dependency Problem:
Have you ever had to change a lot of code because of a new simple requirement? Have you ever had a hard time trying to refactor part of an application? Have you ever been in trouble writing unit tests because of components that required other components?

If you answered yes to any of these questions, maybe your codebase suffers from dependency. It's a typical disease of the code of an application when its components are too coupled. In other words, when a component depends on another one in a too-tight way. The main effect of component dependency is the maintenance difficulty of the code, which, of course, implies a higher cost.


The Dependency Inversion Principle:
The last of the SOLID principles proposes a way to mitigate the dependency problem and make it more manageable. This principle is known as the Dependency Inversion Principle and states that:

High-level modules should not depend on low-level modules. Both should depend on abstractions
Abstractions should not depend on details. Details should depend on abstractions.
You can translate the two formal recommendations as follows: in the typical layered architecture of an application, a high-level component should not directly depend on a lower-level component. You should create an abstraction (for example, an interface) and make both components depend on this abstraction.

Trip in the dependency lingo:
You may have heard many terms and concepts about code dependency, and some of them seem to be very similar and may have been confusing. Well, here is an attempt to give a proper definition of the most common ones:

Dependency Inversion Principle: it's a software design principle; it suggests a solution to the dependency problem but does not say how to implement it or which technique to use.

Inversion of Control (IoC): this is a way to apply the Dependency Inversion Principle. Inversion of Control is the actual mechanism that allows your higher-level components to depend on abstraction rather than the concrete implementation of lower-level components.
Inversion of Control is also known as the Hollywood Principle. This name comes from the Hollywood cinema industry, where, after an audition for an actor role, usually the director says, don't call us, we'll call you.

Dependency Injection: this is a design pattern to implement Inversion of Control. It allows you to inject the concrete implementation of a low-level component into a high-level component.

IoC Container: also known as Dependency Injection (DI) Container, it is a programming framework that provides you with an automatic Dependency Injection of your components.

Dependency Injection approaches:

# Constructor Injection: with this approach, you create an instance of your dependency and pass it as an argument to the constructor of the dependent class.

# Method Injection: in this case, you create an instance of your dependency and pass it to a specific method of the dependent class.

# Property Injection: this approach allows you to assign the instance of your dependency to a specific property of the dependent class.

Spring’s Dependency Injection Container
Spring Framework, at its core, is a dependency injection container that manages the classes you wrote and their dependencies for you.