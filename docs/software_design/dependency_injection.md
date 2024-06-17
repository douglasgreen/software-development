# Dependency Injection

Make all new classes in your top-level code, not inside functions, then inject as parameters.

This can't be done with factory methods because linters complain about static calls. You don't need
fancy DI methods or containers.

An exception is a class that is created inside a class with local arguments not available outside
the class. These need not be injected.

Another exception is a unit test class, which can do their own setup.
