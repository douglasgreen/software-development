# Namespace Guidelines

This guide provides best practices for naming and organizing namespaces,
tailored for professional programmers. By following these conventions, code
readability and maintainability are enhanced.

## Utility namespace

1. **Purpose**: The `Utility` namespace is reserved for classes that contain
   only static methods.
2. **Method Type**: Ensure every method within a `Utility` namespace is static.
3. **Rule of Separation**: Do not mix static and non-static methods in the same
   class. Classes outside the `Utility` namespace should primarily contain
   non-static methods.

## Naming conventions

1. **Singular Names**: Always use singular names for namespaces, e.g., `File`
   rather than `Files`.
2. **Abstract Naming**: When possible, prefer abstract or functional naming for
   namespaces. For example:
    - Place the `Validator` class inside the `Validation` namespace.
    - Use `Routing\Router` instead of simply `Router`.
3. **Descriptive Naming**: Namespaces can also describe what they manage or the
   action they perform. To help decide on a name, fill in the blank for the
   statement: "I am doing **\_**" or "I am managing a/an **\_**". For instance:
    - For file-related functionality, use the `File` namespace.
    - For database management, consider the `Database` namespace.

By adhering to these conventions, developers can easily navigate and understand
the purpose and organization of various namespaces in a project.

<!-- DSG/ChatGPT 7/25/2023 -->
