# Dependency Injection

Consider making all new classes in your top-level code, not inside functions, then inject as
parameters.

You don't need fancy DI methods or containers.

An exception is a class that is created inside a class with local arguments not available outside
the class. These need not be injected.

Another exception is a unit test class, which can do their own setup.

## Discussion

Here are some key considerations for deciding between dependency injection and creating objects
inside methods:

### Key Principles

-   Use dependency injection for objects that represent core dependencies or services needed by a
    class to perform its main responsibilities.

-   Create objects directly inside methods for more transient or implementation-specific objects
    that don't represent core dependencies.

-   Inject abstractions (interfaces/abstract classes) rather than concrete implementations to allow
    for flexibility and easier testing.

-   Consider the lifetime and scope of the object - longer-lived objects that are shared across the
    application are better candidates for injection.

### When to Use Dependency Injection

-   For core services and dependencies that the class needs to function
-   For objects that may have different implementations or need to be mocked in tests
-   For shared resources or objects with longer lifetimes
-   When you want to decouple the class from the creation of its dependencies

### When to Create Objects Directly

-   For simple value objects or data transfer objects
-   For implementation-specific helper objects used only within a method
-   For short-lived objects that don't need to be shared or mocked
-   When creating the object doesn't introduce tight coupling or make testing difficult

### Key Considerations

-   Will this object need to be replaced with a different implementation?
-   Does this object represent a core dependency of the class?
-   Will I need to mock this object in unit tests?
-   Is this a shared resource or a transient object?
-   Does creating this object directly introduce tight coupling?

### Best Practices

-   Use constructor injection as the primary method of dependency injection
-   Inject abstractions rather than concrete types
-   Don't overuse dependency injection - only inject what's necessary
-   Consider using a dependency injection container to manage object lifetimes and injection

The goal is to strike a balance - use dependency injection where it provides clear benefits in terms
of flexibility, testability and decoupling, but avoid overcomplicating things by injecting every
single object. Focus on injecting the core dependencies that define the key responsibilities of the
class.
