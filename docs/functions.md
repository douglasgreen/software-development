# Function Usage

## What are functions and why are they important?

Functions are like mini-programs within a program, designed to perform a
specific task. Here's why they're essential:

1. **Reusability**: Instead of writing the same code multiple times, you can
   write it once inside a function and call that function whenever needed.
2. **Clarity**: Functions replace complex blocks of code with a simple name,
   making your code easier to read.
3. **Testing**: Functions allow for unit testing, ensuring each part of your
   code works correctly.
4. **Efficiency**: While functions make code more organized, remember there's a
   slight performance cost every time a function is called due to the process of
   passing arguments and returning values.

However, not all code needs to be inside a function. Sometimes, it's more
straightforward to have the code run directly.

## When should you use a function?

Consider creating a function when:

1. **Complexity**: The task is intricate, and by placing it inside a function,
   you can test and reuse it.
2. **Repetition**: The same set of instructions appears in multiple places.
3. **Modularity**: You want to make your code more structured, allowing you to
   read a series of high-level actions instead of diving into code details.
4. **Data Handling**: Using functions can simplify interactions with data
   structures.

## When might you avoid using a function?

Not all situations warrant a function. You might skip it when:

1. **Simplicity**: The task can be achieved with a single line of code.
2. **One-time Use**: The code segment isn't reused elsewhere.
3. **Flow Disruption**: Inserting a function might disrupt the natural flow of
   your main code.
4. **Ambiguity**: If the function's purpose isn't clear or it doesn't represent
   a distinct task.

## Best practices for using functions

1. **Naming**: Use action words for function names. For instance, `display()` in
   `Report::display()` implies showing a report.
2. **Single Responsibility**: Ensure your function performs only one task. Avoid
   names with "and" or "or" as they suggest multiple responsibilities.
3. **Brevity**: A function name is a cue, not an exhaustive description. It
   should be concise yet distinct within its context.
4. **Access Levels**: Only make functions public if they need to be accessed
   externally. If a function is a helper or intermediary step, consider making
   it protected.
5. **Size Matters**: As suggested by Steve McConnell in "Code Complete",
   functions should ideally be under 200 lines. If a function grows too large,
   consider breaking it into smaller sub-functions.

Remember, the goal is to make your code more readable, maintainable, and
efficient. Whether you choose to use a function or not should align with these
objectives.

<!-- DSG/ChatGPT 7/23/2023 -->
