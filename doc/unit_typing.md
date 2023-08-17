# Proposal for Unit Typing in Programming Languages
 

Programming often employs two primary methods of type declaration:
* **Static Typing**: Here, variable types like `int`, `float`, and `string` are declared beforehand.
* **Dynamic Typing**: In this approach, variable types are not pre-declared and can change during runtime.

## The Challenge with Existing Typing Mechanisms

1. **Static Typing**: One significant limitation with static typing, especially for floats, is the absence of unit specification. All float numbers are essentially treated as mere numbers without any associated unit. This lack of unit specificity is primarily for the compiler's convenience, which means no built-in unit checks.
2. **Dynamic Typing**: Dynamic typing is even more flexible regarding type specification, often leaving more room for error.

While some languages offer the creation of custom types by aliasing base types (for instance, defining 'miles' or 'hours' as a float), it's still a workaround rather than a native solution.

## The Potential of Predefined Unit Typing

Imagine a programming language equipped with native support for predefined unit typing. Such a language would inherently recognize a vast range of units across diverse measurement systems.

### Features:

1. **Base Units**: The language would natively define basic units like 'miles', 'hours', etc.
2. **Composite Units**: Beyond base units, the language would also acknowledge composite units such as 'miles per hour' (mph). The relationships between these units, whether through division, multiplication, or other operations, would be natively supported.
3. **Arithmetic Validation**: Programmers performing arithmetic on these units would benefit from the compiler's ability to check the validity of these operations based on unit relationships.

### Added Specifications:

1. **Value Ranges**: Define valid value ranges for specific units to ensure logical operations.
2. **Operation Restrictions**: Some values might be defined to be non-multiplicative or restricted from specific operations.

### Example

```
miles m = 100;
hours h = 2;
mph v;

v = m / h;
```

## Real-World Implications

Using a language with built-in unit typing can prevent catastrophic mistakes stemming from unit discrepancies. A historical example is NASA’s Mars Climate Orbiter that was lost in 1988. The Orbiter entered the Mars atmosphere at an incorrect angle due to a unit conversion error. Having predefined unit typing in the programming language could have potentially prevented such an error. While unit tests and specific range checks are also essential in such scenarios, predefined unit typing could significantly simplify the process and reduce error potential for developers.

<!-- DSG/ChatGPT 8/17/2023 -->
