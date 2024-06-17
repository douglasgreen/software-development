### Software Design Patterns and When to Use Them

Design patterns are categorized into three main types: Creational, Structural, and Behavioral. Each
type addresses different aspects of software design and provides solutions to common problems.

#### Creational Design Patterns

1. **Singleton**

    - **Use When**: You need to ensure that a class has only one instance and provide a global point
      of access to it.
    - **Example**: Managing a connection to a database.

2. **Factory Method**

    - **Use When**: You need to create objects without specifying the exact class of object that
      will be created.
    - **Example**: Creating different types of documents in a word processor.

3. **Abstract Factory**

    - **Use When**: You need to create families of related or dependent objects without specifying
      their concrete classes.
    - **Example**: Creating UI components for different operating systems.

4. **Builder**

    - **Use When**: You need to construct a complex object step by step.
    - **Example**: Building a complex configuration for an application.

5. **Prototype**
    - **Use When**: You need to create new objects by copying an existing object, known as the
      prototype.
    - **Example**: Creating a new instance of a graphic object in a drawing application.

#### Structural Design Patterns

1. **Adapter**

    - **Use When**: You need to allow incompatible interfaces to work together.
    - **Example**: Integrating a new class that doesn't match the existing interface.

2. **Bridge**

    - **Use When**: You need to separate an object’s abstraction from its implementation so that the
      two can vary independently.
    - **Example**: Separating the interface and implementation of a remote control and TV.

3. **Composite**

    - **Use When**: You need to treat individual objects and compositions of objects uniformly.
    - **Example**: Representing a hierarchy of UI components.

4. **Decorator**

    - **Use When**: You need to add responsibilities to objects dynamically.
    - **Example**: Adding scrollbars to a window.

5. **Facade**

    - **Use When**: You need to provide a simplified interface to a complex subsystem.
    - **Example**: Providing a simple interface to a complex library.

6. **Flyweight**

    - **Use When**: You need to minimize memory usage by sharing as much data as possible with
      similar objects.
    - **Example**: Managing a large number of fine-grained objects like characters in a text editor.

7. **Proxy**
    - **Use When**: You need to provide a surrogate or placeholder for another object to control
      access to it.
    - **Example**: Implementing lazy initialization or access control.

#### Behavioral Design Patterns

1. **Chain of Responsibility**

    - **Use When**: You need to pass a request along a chain of handlers.
    - **Example**: Handling events in a GUI framework.

2. **Command**

    - **Use When**: You need to encapsulate a request as an object, thereby allowing for
      parameterization and queuing of requests.
    - **Example**: Implementing undo functionality in an application.

3. **Interpreter**

    - **Use When**: You need to define a grammar for a language and interpret sentences in the
      language.
    - **Example**: Parsing and evaluating expressions in a scripting language.

4. **Iterator**

    - **Use When**: You need to provide a way to access elements of a collection sequentially
      without exposing its underlying representation.
    - **Example**: Iterating over elements in a collection like a list or a set.

5. **Mediator**

    - **Use When**: You need to reduce the complexity of communication between multiple objects.
    - **Example**: Managing communication between different components in a chat application.

6. **Memento**

    - **Use When**: You need to capture and restore an object's internal state.
    - **Example**: Implementing undo functionality.

7. **Observer**

    - **Use When**: You need to notify multiple objects about state changes.
    - **Example**: Implementing a publish-subscribe mechanism.

8. **State**

    - **Use When**: You need to allow an object to alter its behavior when its internal state
      changes.
    - **Example**: Managing the state of a TCP connection.

9. **Strategy**

    - **Use When**: You need to define a family of algorithms and make them interchangeable.
    - **Example**: Implementing different sorting algorithms.

10. **Template Method**

    - **Use When**: You need to define the skeleton of an algorithm in a method, deferring some
      steps to subclasses.
    - **Example**: Implementing a framework where the main algorithm is fixed but steps can be
      customized.

11. **Visitor**
    - **Use When**: You need to define a new operation on a class without changing the class.
    - **Example**: Performing operations on nodes in a tree structure.

These patterns provide a structured approach to solving common design problems, making your code
more flexible, reusable, and easier to maintain.
