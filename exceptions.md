## Exceptions in PHP

Exceptions are primarily intended to handle unforeseen or exceptional situations in your code. They shouldn't be used for regular flow control which is better served by conditional statements and loops.

### When should a function throw exceptions in PHP?

* **Invalid Function Arguments:** Throw an exception if a function gets arguments that are out of bounds or inconsistent with what's expected.
* **Resource Unavailability:** If your PHP code anticipates a certain resource (like a database connection, file, or an external service) to be present and it isn't, consider throwing an exception.
* **Failure to Execute Essential Tasks:** If a crucial task fails (e.g., a database query not executing or an inability to write to a file), an exception should be thrown.
* **Unexpected States:** If your PHP application ends up in an unexpected condition, such as when a variable isn't of the anticipated type or value, or if a class property gets accessed before being set, it's wise to throw an exception.

### When should a function log an error in PHP?

The problem with exceptions is that they are intrusive. They stop the program and unwind the stack.

If debugging information is required but the error is not considered to be severe, another option is to log the error rather than throwing the exception. This can be done with the `error_log()` function.

### When should a function in PHP return null?

A function might opt to return null in some circumstances:

* **API Design:** When the API is purposefully crafted to yield null under particular scenarios such as an unset variable.
* **Undesirable Defaults:** For functions that return single values, it might be preferable to return null rather than a default or empty instance. Default values may conceal issues or establish intricate dependencies.
* **Anticipated Lack of Results:** If a function, like a search method, often doesn't find what it's looking for, returning null might be more fitting than throwing an exception. For instance, a null result for a user query on an item that isn't present could be more logical.
* **Ignorable Null Conditions:** Sometimes, a PHP application can overlook null objects, like when processing database records where some bad records lead to null outcomes. Here, logging the anomaly or flagging it in the UI might suffice.

However, be cautious when opting to return null. Unhandled nulls can result in `NullPointerExceptions` which lack clarity. The need for added null checks can also increase the complexity of the code. So, you might want to think about other alternatives like using the Null Object pattern or indeed, throwing exceptions.

### When to define a custom exception subclass in PHP?

Crafting custom exception subclasses in PHP can be beneficial for:

* **Error Differentiation:** By defining exception subclasses, you can differentiate, throw, and catch varied exceptions based on the error's nature. As an analogy, Java has distinct exceptions for file-related issues - `FileNotFoundException` and `IOException`. Similarly, in PHP, different exceptions can help categorize errors.
* **Structured Error Management:** Custom exceptions enable a structured way of error handling. Instead of depending on error codes or other makeshift solutions, you can interrupt the script's normal flow and pass control to a designated exception handler when an exception arises.
* **Enhanced Error Information:** Custom exception subclasses in PHP can be packed with error specifics like the error message, file location, line number, and stack trace, aiding developers in troubleshooting.
* **Improved Code Readability:** Custom exceptions can make your PHP code more understandable by assigning descriptive names to potential errors. This can lead to more self-explanatory and maintainable code.

As a well-behaved code library, PageMaker uses its own base exception class everywhere so its exceptions can be distinguished.

<!-- DSG/ChatGPT 7/25/2023 -->
