# Unit Testing

Unit testing is an essential software development practice, ensuring that
individual units of code (usually functions or methods) operate correctly.
Proper unit testing aids in catching issues early in the development lifecycle,
making software maintenance more manageable.

## Guidelines for effective unit testing

1. **Minimalistic Public Interface**: Do not decompose functions solely for unit
   testing purposes. Refrain from exposing internal functions in the public
   interface just to make them testable. This can clutter the API, making it
   confusing for users.
2. **Approaches to Writing Tests**:
    - **Test-Driven Development (TDD)**: This approach advocates writing tests
      before the actual code. It's beneficial for ensuring code is testable by
      design and can be especially useful for those who might neglect tests if
      left until later. When following TDD, the iterative process is:
        1. Write a failing test.
        2. Implement code to pass the test.
        3. Refactor if necessary.
    - **Testing Legacy Code**: While TDD emphasizes testing before coding,
      sometimes you'll deal with legacy code that wasn't designed with testing
      in mind. In such scenarios, you might need to refactor the code to make it
      testable. Remember, refactoring doesn't mean changing the software's
      behavior but restructuring code to improve its internal structure.
3. **Comparing Test-Driven Development and User-Centered Development**:
    - **Test-Driven Development**: TDD prioritizes creating testable code. It's
      all about ensuring the functionality is solid, reliable, and error-free.
    - **User-Centered Development (UCD)**: UCD puts the user at the center of
      the development process. It employs user stories and use cases to ensure
      that the software meets the end user's needs and provides a satisfactory
      user experience.

## Best practices for unit testing

-   **Isolation**: Each unit test should focus on a singular unit of code.
    External dependencies like databases or APIs should be mocked or stubbed.
-   **Automate Your Tests**: Automation ensures that tests are run consistently
    and can be integrated into your CI/CD pipeline. This way, any code changes
    can be immediately validated.
-   **Write Clear, Descriptive Test Names**: The test name should indicate its
    intent and what behavior is being tested. This helps in quick debugging when
    a test fails.
-   **Keep Tests DRY**: Just like your main codebase, avoid redundancy in your
    tests. Reuse setup and teardown code where applicable.
-   **Test the Positive and Negative**: Test not only the expected outcomes but
    also the edge cases and potential failure modes.
-   **Use Assertions Effectively**: Assertions are the conditions that a test
    checks. Be clear and specific about what you're asserting to ensure accurate
    test results.
-   **Maintain Your Test Code**: As your application evolves, so should your
    tests. Regularly review and update tests to align with the current state of
    your application.

In conclusion, unit testing is an investment in your software's future. While it
may seem time-consuming initially, the dividends it pays in terms of code
reliability, ease of maintenance, and overall software quality are immense.

## Unit testing and design considerations

Unit testing is a fundamental aspect of software development, guiding and
shaping the design of your code. As a developer, when designing any piece of
software, one crucial question you should ask is: "How can this be unit tested?"

Adopting a test-driven development (TDD) approach, where tests are written
before the code itself, naturally aligns your design with this principle.
However, even if you don't strictly adhere to TDD, the implications of unit
testing on your design should always be top of mind.

### Static data and methods

Consider the implications of static data and methods in unit testing:

-   **Static Data**: Using static data can pose challenges in unit testing.
    Since static data retains its state across tests, resetting its values
    between tests becomes difficult. This could lead to unpredictable test
    outcomes. To ensure that unit tests are isolated and reliable, it's
    advisable to minimize the use of static data.
-   **Static Methods**: Static methods, on the other hand, are generally
    favorable for unit testing, provided they do not manipulate static data. In
    fact, they can be more straightforward to test compared to instance methods
    since there's no need to instantiate the class to test the method. Common
    examples include mathematical functions or string manipulation methods.
    These are functions that typically take input values, process them, and
    return an output without any side effects or preconditions, making them
    ideal candidates for unit testing.

In summary, as you design your software, ensure that it's structured in a way
that makes unit testing feasible and straightforward. This not only enhances the
quality of your software but also makes future maintenance and debugging more
efficient.

<!-- DSG/ChatGPT 8/1/2023 -->
