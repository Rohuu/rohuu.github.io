---
title: "How Spring Boot Application Works Internally ?"
written by: "Rohit Singh Bhandari"
date: 2023-07-01T17:15:22+05:30
draft: false
---

## Introduction:<br>

Spring Boot is a powerful framework for building Java applications with ease. It simplifies the development process by providing pre-configured dependencies and reducing the need for manual configuration. In this blog, we will explore the internal workings of a Spring Boot application and how it handles the configuration and initialization process.

## Dependency Management:<br>

Spring Boot relies on pre-configured JAR files to handle various functionalities. These JAR files are specified in the META-INF/spring.factories file. To enable these pre-configured JARs, we need to define the dependencies in the pom.xml file. For example, by adding the spring-boot-starter-data-jpa dependency, we can load all the JARs related to JPA repositories.

## Conditional Configuration:<br>

Spring Boot uses annotations like @ConditionalOnBean, @ConditionalOnClass, and @ConditionalOnMissingBean to conditionally enable or disable certain configurations. These annotations help determine whether a specific configuration should be applied based on the presence or absence of certain conditions. For example, @ConditionalOnBean(DataSource.class) ensures that the JpaRepositoriesAutoConfiguration is enabled only if a DataSource bean is available.

**The @SpringBootApplication Annotation:**
The @SpringBootApplication annotation is the main annotation used in a Spring Boot application. It combines three essential annotations: *@SpringBootConfiguration, @EnableAutoConfiguration and @ComponentScan*. Let's take a closer look at each of these annotations:

**@SpringBootConfiguration:** 
This annotation indicates that the class contains Spring Boot configuration. It is similar to the @Configuration annotation and acts as a bean.

**@EnableAutoConfiguration:** 
This annotation enables automatic configuration of beans based on certain conditions. It leverages the @Conditional annotations we discussed earlier to determine which configurations to enable.

**@ComponentScan:** 
This annotation scans the specified classes and packages to create beans. It is responsible for detecting classes annotated with @Component, @Service, @Configuration, and other similar annotations.

## The run() Method:<br>

The run() method is a crucial part of the Spring Boot application. It kickstarts the main application context and initializes all the declared beans in the configuration classes. Here's a high-level flow of what happens within the run() method:

* Create application context: The main application context is created, and it searches for classes annotated with @Configuration.

* Check application type: The application type, such as SERVLET or REACTIVE, is determined based on the context type.

* Register annotated class beans: The beans declared in the annotated classes (e.g., @Component, @Service, @Configuration) are registered with the context.

* Configuration and initialization: The necessary configurations are performed, including setting up the dispatcher servlet, registering default handler mappings, message converters, and other basic components.

* Embedded server deployment: Spring Boot supports multiple embedded servers like Tomcat, Jetty, and Undertow. The application deploys itself using an embedded server, such as TomcatEmbeddedServletContainer, which automatically adds the context and deploys the JAR or WAR file.

## Some other important Spring annotations:
In addition to the @SpringBootApplication annotation, Spring Boot provides several other important annotations that help streamline the development process and enhance the functionality of your application. Here are some notable Spring Boot annotations:

**@RestController:**<br>
This annotation is used to mark a class as a RESTful controller. It combines the @Controller and @ResponseBody annotations, simplifying the creation of RESTful APIs. It eliminates the need to annotate each individual handler method with @ResponseBody by default.

**@RequestMapping:**<br>
This annotation is used to map HTTP requests to specific handler methods within a controller class. It can be applied at both the class and method levels to define the URL paths and HTTP methods that the handler methods should respond to.

**@Autowired:**<br>
The @Autowired annotation is used to automatically wire beans by type. It can be applied to fields, constructors, or setter methods. Spring Boot's dependency injection mechanism uses this annotation to resolve and inject dependencies automatically.

**@Value:**<br>
The @Value annotation is used to inject values from external sources, such as properties files or environment variables, into Spring beans. It can be applied to fields or method parameters, allowing you to easily configure and customize your application.

**@ConfigurationProperties:**<br>
This annotation is used to bind external configuration properties to a Java bean. By defining a class with this annotation and specifying the prefix of the properties, you can easily map and access the properties within your application.

**@EnableCaching:**<br>
This annotation is used to enable caching in Spring Boot applications. By adding this annotation to your configuration class, you can take advantage of Spring's caching abstraction and cache results of expensive operations, improving performance.

**@EnableScheduling:**<br>
The @EnableScheduling annotation is used to enable scheduled task execution in Spring Boot applications. By annotating a configuration class with this annotation, you can define scheduled methods using the @Scheduled annotation and specify the timing and frequency of their execution.

**@EnableAsync:**<br>
This annotation is used to enable asynchronous method execution in Spring Boot applications. By adding this annotation to your configuration class, you can annotate methods with the @Async annotation to execute them asynchronously, leveraging the benefits of parallel processing.

**@EnableTransactionManagement:**<br>
The @EnableTransactionManagement annotation enables Spring's transaction management capabilities in your application. By adding this annotation to your configuration class, you can use declarative transaction management with the @Transactional annotation to handle database transactions easily.

**@Bean**<br>
When you annotate a method with @Bean, it tells Spring that the method should be used to create and configure a bean. The return value of the method becomes the bean instance, and its name is derived from the method name unless specified explicitly.

```java
    @Configuration
    public class MyConfiguration {

        @Bean
        public MyBean myBean() {
            return new MyBean();
        }

        // Other configuration methods...

    }
```


## Conclusion:<br>

Understanding the internal working of a Spring Boot application can help developers utilize its power and convenience effectively. We explored the role of pre-configured JARs, conditional configuration, the @SpringBootApplication annotation, and the run() method. With this knowledge, you can dive deeper into Spring Boot and build robust and scalable applications more efficiently.