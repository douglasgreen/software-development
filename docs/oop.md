# Object-Oriented Programming

## Object-oriented design

Object-oriented design (OOD) is a methodology that revolves around designing
software systems as a collection of interacting objects. Here's a summary of the
best practices of OOD:

**1. How do we define objects?**

-   **Encapsulation**: Objects should encapsulate data (attributes) and the
    methods (functions) that operate on the data. This means the internal
    representation of an object is hidden from the outside, and only the object
    can interact with its internal data.
-   **Responsibility-Driven Design**: When defining objects, think about their
    responsibilities. An object should have a clear responsibility or set of
    responsibilities, and it shouldn't do too much.
-   **Cohesion**: Objects should have a single, well-defined purpose or
    functionality. A highly cohesive object performs a single task or a closely
    related group of tasks.

**2. When should inheritance be used?**

-   **Is-A Relationship**: Inheritance should represent an "is-a" relationship.
    For instance, a "Car" is a "Vehicle". It should not be used just to reuse
    code.
-   **Reuse and Extension**: Inheritance allows subclasses to reuse
    functionality from parent classes and also extend or override specific
    behaviors.
-   **Liskov Substitution Principle (LSP)**: Subclasses should be substitutable
    for their base classes. This means that if a piece of code is designed to
    work with an instance of the base class, it should work with any of its
    derived classes without knowing it.
-   **Avoid Deep Inheritance Hierarchies**: Deeply nested inheritance can lead
    to confusion and unintended side effects. Prefer shallow hierarchies and
    composition where possible.

**3. How do beginners focus too much on object design?**

-   **Overengineering**: Beginners often make designs overly complex by trying
    to anticipate all potential future needs. It's essential to focus on current
    requirements and refactor later as needs evolve.
-   **Misuse of Inheritance**: As opposed to using composition, beginners tend
    to overuse inheritance as a tool for code reuse. In many cases, favoring
    composition (combining simple objects to build more complex ones) can be
    more flexible and maintainable.
-   **Overemphasis on Patterns**: While design patterns are valuable tools,
    beginners can sometimes apply them inappropriately or where they're not
    needed, leading to unnecessary complexity.
-   **Not Embracing Simplicity**: The simplest solution that meets the current
    need is often the best one. Over-designing or trying to abstract too early
    can lead to confusion and maintenance challenges later.

**Other Best Practices**:

-   **Polymorphism**: This allows objects of different classes to be treated as
    objects of a common super class. Useful for creating more generic and
    reusable code.
-   **Open/Closed Principle**: Software entities (classes, modules, etc.) should
    be open for extension but closed for modification. This means that you can
    add new functionality without changing existing code.
-   **Separation of Concerns**: Different functionalities should be separated
    into different classes or modules. This makes the system more modular and
    easier to maintain.
-   **Loose Coupling**: Objects should not be overly dependent on each other.
    This can be achieved through interfaces, dependency injection, and other
    design patterns.
-   **DRY (Don't Repeat Yourself)**: Reuse code as much as possible. Avoid
    redundancy.

In conclusion, object-oriented design is about creating clear, maintainable, and
scalable systems by thinking in terms of objects, their responsibilities, and
their interactions. Adopting these best practices can ensure that designs are
robust and sustainable over time.

## Inheritance of features

Object-oriented inheritance can be problematic for designing features because it
enforces a rigid hierarchy for adding new features. Each set of new features
must strictly build upon an existing set of features, making it challenging to
define features as independent collections.

For instance, suppose you have features A, B, and C, and you add each new
feature through an inheritance chain with a class of the same name. In that
case, you cannot access feature C without inheriting features B and A. However,
if you opt for a simple class D with features A, B, and C, each feature can be
toggled on or off as required. This example demonstrates how inheritance is
often overused as a design solution.

To avoid such limitations and foster more flexibility, it is crucial to consider
alternative approaches like composition or interfaces. These methodologies allow
you to create feature modules that can be combined in various ways, enabling a
more modular and adaptable design.

By using composition, you can build classes with a collection of features, where
each feature operates independently and can be used in different combinations as
needed. This way, you have the freedom to assemble features in any manner
without being bound by a strict hierarchy.

In summary, while object-oriented inheritance has its advantages, it is
essential for professional programmers to be cautious about its use and consider
other design patterns that offer greater flexibility and modularity for feature
implementation. By doing so, you can create more maintainable and adaptable
software systems.

### Occam's Razor

Occam's Razor is a philosophical and scientific principle that suggests that
given multiple explanations for a phenomenon, the simplest one is likely the
correct one, as long as it fully explains the observed data. In other words, one
should not make more assumptions than are necessary.

When applied to Object-Oriented Design (OOD), Occam's Razor can guide developers
in several significant ways:

1. **Simplicity Over Complexity**: When designing classes, methods, or
   inheritance hierarchies, aim for the simplest design that satisfies the
   requirements. Avoid unnecessary features or complexities that don't serve a
   clear purpose.
2. **Prefer Composition Over Inheritance**: While inheritance is a powerful
   feature of OOD, it can sometimes introduce unnecessary complexity, especially
   deep inheritance hierarchies. Often, using composition (combining objects)
   can offer a simpler and more flexible solution.
3. **Avoid Premature Optimization**: Developers sometimes anticipate potential
   future needs or performance issues and introduce complexity to address them
   ahead of time. However, without clear data indicating a need for such
   optimizations, it's often better to stick with a simpler design and refactor
   later if necessary.
4. **Minimalistic Class Design**: Only include methods and attributes in a class
   that are essential to its responsibility. Don't add functions or data points
   just because they "might" be useful in the future.
5. **Reduce Dependencies**: A system where components are heavily interdependent
   can be complex and hard to maintain. Aim for designs where components are
   loosely coupled, which often results in a simpler and more modular system.
6. **Clear and Concise Code**: Occam's Razor can also apply directly to coding.
   Write code that's straightforward and easy to understand. Avoid convoluted
   logic or "clever" code that can be hard to follow and maintain.
7. **Refactoring**: As software evolves, it's not uncommon for code to become
   more complex over time. Regularly revisit and refactor code to ensure that it
   remains as simple as possible while still meeting its requirements.

In essence, Occam's Razor is a call for simplicity and clarity. When applied to
OOD, it pushes for designs that are straightforward, easy to understand, and
maintainable. By continuously questioning whether a design or piece of code
could be made simpler, developers can create more robust and sustainable
software.

## Overview of interfaces

Interfaces establish a contract between classes, ensuring that certain methods
are implemented. They enhance code flexibility and play a crucial role in
dependency injection.

## Purpose of an interface

1. **Flexibility:** An interface allows objects of different classes to be
   treated uniformly, facilitating polymorphism.
2. **Dependency Injection:** It enables injecting specific implementations into
   classes, promoting code modularity and testability.

## Methods in interfaces

1. **Inclusion:** All methods or method arguments that a caller may use should
   be part of the interface. Omitting these would lead to errors.
2. **Focus on Outputs:** Emphasize the results or services an interface provides
   rather than the inputs.
3. **Service Methods:** Prefer methods like `render()` over getters that merely
   fetch data. Avoid specifying setters; the implementing class can determine
   how to set data.
4. **Consistency:** Document argument and return types to ensure uniform
   implementation across classes. Highlight expected exceptions.
5. **No Optional Arguments:** Exclude optional method arguments from interface
   declarations.

## Organization and naming

1. **Location:** Interfaces are placed in the `Contract` namespace, emphasizing
   their role as generalized contracts, not tied to specific class
   implementations.
2. **Naming Convention:**
    - Interface: `PageMaker\Contract\Request`
    - Implementation: `PageMaker\Request`

## Interfaces vs. abstract classes

1. **Interfaces:** Provide method signatures without imposing any structure or
   behavior, allowing complete extensibility.
2. **Abstract Classes:** Offer a blend of predefined (yet potentially
   incomplete) behavior and unimplemented methods. Examples include a general
   `Widget` class.

## Implementing an interface

1. **Consistency:** The implementing class should not have extra public methods
   beyond what the interface defines, except for the constructor.
2. **Aliasing:** To use an interface and its implementation concurrently, alias
   them, e.g., `use PageMaker\Contract\Registry as RegistryInterface`.

## Class design principles

### Access modifiers

1. **Flexibility:** Use `protected` or `public` to ensure class members can be
   extended by subclasses. Avoid private members which can't be overridden.

### Method organization

1. **Modularity:** Decompose large functions into smaller, more manageable
   pieces to enhance extensibility.
2. **Type-Checking:** Balance strict type-checking with input flexibility.
3. **Setup:** Ensure classes are easy to set up, well-documented, and intuitive.

### Class naming

1. **Simplicity:** Avoid redundant words like "Manager" or "Handler."
2. **PSR Naming:** For abstract classes, use the format: `Abstract<name>`.
   Interfaces don't require the "Interface" suffix and belong in the `Contract`
   directory.

### Design principles

1. **Single Responsibility:** Each class should have a single responsibility.
   Separate I/O, processing, and storage.
2. **Static Calls:** Avoid static calls. Use registries to enable class
   replacements at runtime. Static utility classes are exceptions.
3. **File Structure:**
    - Group by: const > static > instance.
    - Order by access level: public > protected.
    - Logical order: magic methods > setters > getters > finalizers.

### Controllers

Controllers are identified by routers using the pattern: `<page>Controller` with
methods formatted as `get<action>` or `post<action>`.

## Method chaining

All object setter functions should return $this for chaining.

## Properties

Don't set temporary properties. Property should be permanent traits. Instead,
past temporary properties around as arguments or create a new class with the
command pattern that has only temporary properties.

## Program API

What classes and functions to expose? If a class is not used independently,
construct it internally to another class. Consider having a single public class
with chained setters.

<!-- DSG/ChatGPT 7/25/2023 -->
