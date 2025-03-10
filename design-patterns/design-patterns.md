# Design Patterns in Java

Design patterns can be divided into three main categories:

1. **Creational Design Patterns**: These design patterns provide a way to create objects while hiding the creation logic, rather than instantiating objects directly using the new operator. This gives the program more flexibility in deciding which objects need to be created for a given use case.
    - **[Factory Pattern](#factory-pattern)**
    - **Abstract Factory Pattern**
    - **[Singleton Design Pattern](#singleton-design-pattern)**
    - **Builder Pattern**
    - **Prototype Pattern**

2. **Structural Design Patterns**: These design patterns concern class and object composition. The concept of inheritance is used to compose interfaces and define ways to compose objects to obtain new functionalities.
    - **Adapter Pattern**
    - **Bridge Pattern**
    - **Filter Pattern**
    - **Composite Pattern**
    - **Decorator Pattern**
    - **Facade Pattern**
    - **Flyweight Pattern**
    - **Proxy Pattern**

3. **Behavioral Design Patterns**: These design patterns are specifically concerned with communication between objects.
    - **Chain of Responsibility Pattern**
    - **Command Pattern**
    - **Interpreter Pattern**
    - **Iterator Pattern**
    - **Mediator Pattern**
    - **Memento Pattern**
    - **Observer Pattern**
    - **State Pattern**
    - **Null Object Pattern**
    - **Strategy Pattern**
    - **Template Pattern**
    - **Visitor Pattern**

## Factory Pattern

The Factory Design Pattern is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created. This pattern is particularly useful when the exact type of object that needs to be created is determined at runtime.

### Key Concepts

- **Factory Method**: A method that returns an instance of a class.
- **Product**: The interface or abstract class that defines the type of object the factory method will create.
- **ConcreteProduct**: The specific implementation of the Product interface.
- **Creator**: The class that contains the factory method.
- **ConcreteCreator**: The class that implements the factory method to create instances of ConcreteProduct.

### Advantages

- **Encapsulation**: The Factory Design Pattern encapsulates the object creation process, making the code more modular and easier to maintain.
- **Flexibility**: It allows for the creation of objects without specifying the exact class of object that will be created.
- **Scalability**: New types of products can be added without changing the existing code.

### Why Abstract Method is Required and What Happens if We Don't Use Factory Method

The abstract method in the Factory Design Pattern is essential because it defines a contract that must be followed by all subclasses. This ensures that the subclasses provide their own specific implementations of the method, which is crucial for creating different types of objects. Without the abstract method, the superclass would not have a way to enforce this contract, leading to potential inconsistencies and errors in the object creation process.

If we don't use the factory method, the object creation process would be tightly coupled with the client code. This means that any changes to the object creation logic would require changes to the client code as well, making the code less modular and harder to maintain. Additionally, without the factory method, it would be challenging to introduce new types of products without modifying the existing code, reducing the flexibility and scalability of the system.


### Example

Here is a simple example of the Factory Design Pattern in Java:

```java
// Product interface
public interface Product {
    void use();
}

// ConcreteProduct class
public class ConcreteProductA implements Product {
    @Override
    public void use() {
        System.out.println("Using ConcreteProductA");
    }
}

public class ConcreteProductB implements Product {
    @Override
    public void use() {
        System.out.println("Using ConcreteProductB");
    }
}

// Creator class
public abstract class Creator {
    public abstract Product factoryMethod();

    public void doSomething() {
        Product product = factoryMethod();
        product.use();
    }
}

// ConcreteCreator classes
public class ConcreteCreatorA extends Creator {
    @Override
    public Product factoryMethod() {
        return new ConcreteProductA();
    }
}

public class ConcreteCreatorB extends Creator {
    @Override
    public Product factoryMethod() {
        return new ConcreteProductB();
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        Creator creatorA = new ConcreteCreatorA();
        creatorA.doSomething();

        Creator creatorB = new ConcreteCreatorB();
        creatorB.doSomething();
    }
}

```


## Singleton Design Pattern

### What is Singleton Design Pattern?
The Singleton Design Pattern ensures that a class has only one instance and provides a global point of access to it. This is useful when exactly one object is needed to coordinate actions across the system.

### Advantages
1. Controlled access to the sole instance.
2. Reduced namespace usage.
3. Permits refinement of operations and representation.
4. Permits a variable number of instances.
5. More flexible than class operations.

### Disadvantages
1. Can be difficult to test due to global state.
2. Can hide dependencies, making the code less clear.
3. Can be difficult to subclass.
4. Potential for resource contention in multi-threaded environments.

### Why is it required?
Singleton is required when:
1. Exactly one instance of a class is needed to control the action.
2. The sole instance should be extensible by subclassing, and clients should be able to use an extended instance without modifying their code.

### What problem happens if we do not use it?
Without the Singleton pattern, multiple instances of a class can be created, leading to inconsistent behavior, resource wastage, and difficulty in coordinating actions across the system.

### Java Example
public class Singleton {
    // Private static variable of the same class that is the only instance of the class.
    private static Singleton singleInstance = null;

    // Private constructor to restrict instantiation of the class from other classes.
    private Singleton() {
        // Initialization code here
    }

    // Public static method that returns the instance of the class, this is the global access point for outer world to get the instance of the singleton class.
    public static Singleton getInstance() {
        if (singleInstance == null) {
            synchronized (Singleton.class) {
                if (singleInstance == null) {
                    singleInstance = new Singleton();
                }
            }
        }
        return singleInstance;
    }

    // Other methods of the Singleton class
    public void showMessage() {
        System.out.println("Hello World from Singleton!");
    }
}

// Client code to test the Singleton
public class SingletonDemo {
    public static void main(String[] args) {
        // Get the only object available
        Singleton singleton = Singleton.getInstance();

        // Show the message
        singleton.showMessage();
    }
}

### Java Design Patterns Example Tutorial

Design patterns represent the best practices used by experienced object-oriented software developers. Design patterns are solutions to general problems that software developers faced during software development. These solutions were obtained by trial and error by numerous software developers over quite a substantial period of time.



