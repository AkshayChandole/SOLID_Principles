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
![ocp1](https://github.com/user-attachments/assets/06dbe1cd-e5a1-4894-bbd9-0fce5841ac1c)

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
![ocp2](https://github.com/user-attachments/assets/e13c12b8-9000-4f32-afbb-17c2219552ee)


In the refactored example, the `Shape` interface defines a `calculateArea` method. Both `Rectangle` and `Circle` implement this interface. The `AreaCalculator` class now depends on the `Shape` interface, allowing it to calculate the area of any shape without modification. This adheres to the Open/Closed Principle by allowing the system to be extended with new shapes without altering existing code.

### Benefits of OCP

-   **Enhanced Maintainability:** Changes are easier to implement without affecting existing functionality.
-   **Reduced Risk of Bugs:** Adding new functionality does not interfere with existing, tested code.
-   **Improved Extensibility:** New features can be added with minimal effort.

<br>


## Liskov Substitution Principle (LSP)

### Definition

The *Liskov Substitution Principle* states that ***"objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program."*** In other words, if `S` is a subtype of `T`, then objects of type `T` may be replaced with objects of type `S` without altering any of the desirable properties of the program (e.g., correctness).

### Explanation

The Liskov Substitution Principle, introduced by Barbara Liskov in 1987, is one of the five SOLID principles of object-oriented design. It ensures that a subclass can stand in for its superclass without causing errors or unexpected behavior. This principle promotes the use of polymorphism and inheritance correctly.

For a subclass to be a true substitute for its superclass:
- It should not remove base class behavior expected by the client code.
- It should not violate the invariants of the base class.
- It should follow the contract established by the base class.

### Examples

#### Example 1: Before Applying LSP

```java
// Bird.java

public class Bird {
    public void fly() {
        System.out.println("Flying");
    }
}
```

```java
// Ostrich.java

public class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostriches cannot fly");
    }
}
```

```java
// BirdWatcher.java

public class BirdWatcher {
    public void watch(Bird bird) {
        bird.fly();
    }
}
```
![lsp1](https://github.com/user-attachments/assets/2a47325d-e56e-4972-b4a5-4e61f2be411b)

In the above example, the `Ostrich` class violates the Liskov Substitution Principle because it cannot fly, and calling `fly()` results in an exception. The `BirdWatcher` class expects all `Bird` instances to be able to fly.

#### Example 2: After Applying LSP

```java
// Bird.java

public abstract class Bird {
    public abstract void move();
}
```

```java
// Sparrow.java

public class Sparrow extends Bird {
    @Override
    public void move() {
        fly();
    }

    private void fly() {
        System.out.println("Flying");
    }
}
```

```java
// Ostrich.java

public class Ostrich extends Bird {
    @Override
    public void move() {
        walk();
    }

    private void walk() {
        System.out.println("Walking");
    }
}
```

```java
// BirdWatcher.java

public class BirdWatcher {
    public void watch(Bird bird) {
        bird.move();
    }
}` 
```
![lsp2](https://github.com/user-attachments/assets/1989b507-7cd5-4259-9ef6-3ce6eda531d4)

In the refactored example, the `Bird` class has an abstract `move` method that is implemented by `Sparrow` and `Ostrich` according to their capabilities. Now, the `BirdWatcher` class can use any `Bird` subclass without worrying about whether it can fly or not.

### Benefits of LSP

-   **Improved Code Reusability:** Classes can be used interchangeably without unexpected behavior.
-   **Enhanced Maintainability:** New subclasses can be added without modifying existing code.
-   **Increased Reliability:** Reduces the risk of runtime errors due to improper subclassing.

<br>

## Interface Segregation Principle (ISP)

### Definition

The Interface Segregation Principle states that ***"no client should be forced to depend on methods it does not use."*** Instead of having one large interface, it is better to have multiple smaller, specific interfaces. This principle ensures that classes only implement the functionality that is essential to them.

### Explanation

The Interface Segregation Principle is one of the five SOLID principles of object-oriented design. It helps in creating a system that is more understandable, maintainable, and flexible by promoting the use of fine-grained interfaces. When interfaces are well-segregated:
- Clients only need to know about the methods that are relevant to them.
- Implementations are easier to understand and modify.
- Changes in one part of the system are less likely to impact other parts.

### Examples

#### Example 1: Before Applying ISP

```java
// Worker.java

public interface Worker {
    void work();
    void eat();
}
```

```java
// HumanWorker.java

public class HumanWorker implements Worker {
    @Override
    public void work() {
        // Human work implementation
    }

    @Override
    public void eat() {
        // Human eating implementation
    }
}
```

```java
// RobotWorker.java

public class RobotWorker implements Worker {
    @Override
    public void work() {
        // Robot work implementation
    }

    @Override
    public void eat() {
        // Robots do not eat, so this method is not needed
        throw new UnsupportedOperationException("Robots do not eat");
    }
}
```
![isp1](https://github.com/user-attachments/assets/be637494-00cc-413e-9b3e-eab7149a1014)

In the above example, the `RobotWorker` class is forced to implement the `eat` method, which it does not need, violating the Interface Segregation Principle.

#### Example 2: After Applying ISP

```java
// Workable.java

public interface Workable {
    void work();
}
```

```java
// Eatable.java

public interface Eatable {
    void eat();
}
```

```java
// HumanWorker.java

public class HumanWorker implements Workable, Eatable {
    @Override
    public void work() {
        // Human work implementation
    }

    @Override
    public void eat() {
        // Human eating implementation
    }
}
```

```java
// RobotWorker.java

public class RobotWorker implements Workable {
    @Override
    public void work() {
        // Robot work implementation
    }
}` 
```
![isp2](https://github.com/user-attachments/assets/a5b7e09c-f40a-4c15-aa03-525a6aa9b039)

In the refactored example, the `Worker` interface is split into `Workable` and `Eatable` interfaces. The `HumanWorker` class implements both interfaces because it needs both methods, while the `RobotWorker` class only implements the `Workable` interface.

### Benefits of ISP

-   **Improved Code Readability:** Smaller interfaces are easier to understand.
-   **Enhanced Maintainability:** Changes in one interface do not affect clients that do not depend on it.
-   **Increased Flexibility:** Classes can implement multiple, specific interfaces based on their needs.


## Dependency Inversion Principle (DIP)

### Definition

[Content for Definition]

### Explanation

[Content for Explanation]

### Examples

[Content for Examples]

## Conclusion

[Content for Conclusion]
