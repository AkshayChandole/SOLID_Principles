# SOLID_Principles

## Table of Contents

1. [Introduction](#introduction)
2. [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
   - [Definition](#definition)
   - [Explanation](#explanation)
   - [Examples](#examples)
3. [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
   - [Definition](#definition-1)
   - [Explanation](#explanation-1)
   - [Examples](#examples-1)
4. [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
   - [Definition](#definition-2)
   - [Explanation](#explanation-2)
   - [Examples](#examples-2)
5. [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
   - [Definition](#definition-3)
   - [Explanation](#explanation-3)
   - [Examples](#examples-3)
6. [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
   - [Definition](#definition-4)
   - [Explanation](#explanation-4)
   - [Examples](#examples-4)
7. [Conclusion](#conclusion)

## Introduction

<p>SOLID is an acronym for the first five object-oriented design (OOD) principles by <strong>Robert C. Martin</strong>, also known as Uncle Bob, the author of Clean Code: A Handbook of Agile Software Craftsmanship. </p>

### Why use SOLID principles ?

Let’s look at the possible issues below that may occur in the code if we don’t adhere to the SOLID principles.

-   The code may become tightly coupled with several components, which makes it difficult to integrate new features or bug fixes and sometimes leads to unidentified problems.
-   The code will be untestable, which effectively means that every change will need end-to-end testing.
    
-   The code may have a lot of duplication.
    
-   Fixing one issue results in additional errors.
    

However, if we adhere to the SOLID principles, we are able to do the following:

-   Reduce the tight coupling of the code, which reduces errors.
    
-   Reduce the code’s complexity for future use.
    
-   Produce more extensible, maintainable, and understandable software code.
    
-   Produce the code that is modular, feature specific, and is extremely testable.

  <br>


## Single Responsibility Principle (SRP)

### Definition

The Single Responsibility Principle states that a ***class should have only one reason to change*** meaning that a class should have only one job or responsibility. This principle helps in reducing the complexity of code and makes it more maintainable and easier to understand.

### Explanation

In object-oriented programming, the Single Responsibility Principle is about designing classes with a single responsibility. When a class has only one reason to change, it means that it is focused on a single task or piece of functionality. This makes the class easier to understand, test, and maintain.

By adhering to SRP, you ensure that your classes are small, cohesive, and focused. This leads to better organization of code and helps in managing dependencies more effectively. When a class is responsible for only one thing, changes in the requirements for that functionality will affect only that class, reducing the risk of introducing bugs in other parts of the system.

### Examples

#### Example 1: Before Applying SRP

```java
public class Employee {
    private String name;
    private String email;

    public Employee(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }

    public void saveToDatabase() {
        // Code to save employee details to database
    }

    public void sendEmail(String message) {
        // Code to send email to employee
    }
}
```

![srp1](https://github.com/user-attachments/assets/a62700ce-7051-495e-80c4-f2f7181e5075)

In the example above, the `Employee` class has multiple responsibilities: managing employee details, saving to the database, and sending emails. This violates the SRP because changes to email functionality or database storage would require modifications to the `Employee` class.

#### Example 2: After Applying SRP
```java
    public class Employee {
        private String name;
        private String email;
    
        public Employee(String name, String email) {
            this.name = name;
            this.email = email;
        }
    
        public String getName() {
            return name;
        }
    
        public String getEmail() {
            return email;
        }
    }
    
    public class EmployeeRepository {
        public void saveToDatabase(Employee employee) {
            // Code to save employee details to database
        }
    }
    
    public class EmailService {
        public void sendEmail(Employee employee, String message) {
            // Code to send email to employee
        }
    }
```

![srp2](https://github.com/user-attachments/assets/ffbaf28c-164e-4f00-8e05-6350924e25c1)

In the refactored example, we have separated the responsibilities into three different classes: `Employee`, `EmployeeRepository`, and `EmailService`. The `Employee` class is now solely responsible for managing employee details, the `EmployeeRepository` is responsible for saving employee details to the database, and the `EmailService` is responsible for sending emails. This adheres to the Single Responsibility Principle and makes the code more modular and easier to maintain.

### Benefits of SRP

-   **Improved Readability:** Code is easier to understand when each class has a single responsibility.
-   **Enhanced Maintainability:** Changes in one responsibility do not affect other parts of the code, making maintenance easier.
-   **Better Testability:** Smaller, focused classes are easier to test.
-   **Reduced Risk of Bugs:** Isolating responsibilities reduces the likelihood of introducing bugs when making changes.

<br>

## Open/Closed Principle (OCP)

### Definition

The Open/Closed Principle states that ***"software entities (classes, modules, functions, etc.) should be open for extension but closed for modification."*** This means that the behavior of a module can be extended without modifying its source code.

### Explanation

The Open/Closed Principle is one of the five SOLID principles of object-oriented design. It helps in creating systems that are easy to extend and maintain. The main idea is that you should be able to add new functionality to existing code without changing the existing code.

By adhering to OCP, you reduce the risk of introducing bugs into existing, tested code when new functionality is added. This principle is typically achieved through polymorphism and abstraction.

### Examples

#### Example 1: Before Applying OCP

```java
// Rectangle.java

public class Rectangle {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }
}
```

```java
// AreaCalculator.java

public class AreaCalculator {
    public int calculateRectangleArea(Rectangle rectangle) {
        return rectangle.getWidth() * rectangle.getHeight();
    }
}
```
In the above example, if we want to calculate the area of a circle, we would need to modify the `AreaCalculator` class, which violates the Open/Closed Principle.

#### Example 2: After Applying OCP
```java
// Shape.java

public interface Shape {
    int calculateArea();
}
```

```java
// Rectangle.java

public class Rectangle implements Shape {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }

    @Override
    public int calculateArea() {
        return width * height;
    }
}
```

```java
// Circle.java

public class Circle implements Shape {
    private int radius;

    public Circle(int radius) {
        this.radius = radius;
    }

    public int getRadius() {
        return radius;
    }

    @Override
    public int calculateArea() {
        return (int) (Math.PI * radius * radius);
    }
}
```

```java
// AreaCalculator.java

public class AreaCalculator {
    public int calculateArea(Shape shape) {
        return shape.calculateArea();
    }
}` 
```

In the refactored example, the `Shape` interface defines a `calculateArea` method. Both `Rectangle` and `Circle` implement this interface. The `AreaCalculator` class now depends on the `Shape` interface, allowing it to calculate the area of any shape without modification. This adheres to the Open/Closed Principle by allowing the system to be extended with new shapes without altering existing code.

### Benefits of OCP

-   **Enhanced Maintainability:** Changes are easier to implement without affecting existing functionality.
-   **Reduced Risk of Bugs:** Adding new functionality does not interfere with existing, tested code.
-   **Improved Extensibility:** New features can be added with minimal effort.

<br>


## Liskov Substitution Principle (LSP)

### Definition

[Content for Definition]

### Explanation

[Content for Explanation]

### Examples

[Content for Examples]

## Interface Segregation Principle (ISP)

### Definition

[Content for Definition]

### Explanation

[Content for Explanation]

### Examples

[Content for Examples]

## Dependency Inversion Principle (DIP)

### Definition

[Content for Definition]

### Explanation

[Content for Explanation]

### Examples

[Content for Examples]

## Conclusion

[Content for Conclusion]
