# Reducing Complexity

## Types of Complexity

There are two types of complexity:

-   Essential complexity
-   Accidental complexity

Essential complexity refers to the inherent difficulty of a task and the necessary effort required
to complete it. Accidental complexity, on the other hand, arises from misunderstandings or
inefficiencies that add unnecessary effort to the task.

Albert Einstein's advice to make a task as simple as possible, but no simpler, emphasizes the
importance of minimizing accidental complexity. However, it's important to note that only accidental
complexity can be reduced to simplify a task without compromising its integrity.

## Limitations of Complexity Measures

The main issue with complexity measures is that they do not distinguish between essential complexity
and accidental complexity. For instance, McCabe's complexity measure evaluates the complexity of
statement constructs but cannot determine if those constructs are essential.

As a result, its typical solution of moving constructs into different functions does not actually
reduce the overall complexity; it merely redistributes it.

## Measuring Across Function Boundaries

We can use `if` statements in a function as an example of failing to reduce complexity. Splitting
`if` statements into separate functions doesn't necessarily make the code simpler.

Consider a single function with 10 `if` statements. This function has \(2^{10} = 1024\) possible
outcomes. Now, if you split it into two functions with five `if` statements each, each function
appears simpler because it has \(2^5 = 32\) possible outcomes.

However, when the first function is called followed by the second function, the total number of
possible outcomes remains the same: \(2^5 \times 2^5 = 32 \times 32 = 1024\).

This approach merely shuffles the code around without actually reducing its complexity. It only
seems to reduce complexity because the measurement is done within each function separately, ignoring
the interactions between functions. This highlights a flaw in the measurement method, showing that
it is not always helpful in assessing true complexity.

## Reducing Complexity

To reduce complexity, you must first distinguish between essential and accidental complexity.

One form of accidental complexity is repetition. The "Don't Repeat Yourself" (DRY) principle
suggests reducing this complexity by avoiding redundancy. For example, if your code has 10 different
ways to display a page header, you can combine them into a single page header function that is
called in 10 places. This reduces the accidental complexity of repeating the same display code
multiple times.

Another form of accidental complexity is disorganization. Imagine writing a 10-page essay as a
series of unstructured paragraphs. To reduce this complexity, you should break the essay into
subtopics and label each subtopic with a heading. To further simplify, provide a table of contents.
This makes the essay easier to describe and understand by breaking it into manageable sections.

In source code, similar activities include:

1. **Adding comments**: Like subtopic headings, comments label each section of code, and enable you
   to organize related code into sections with only one purpose.
2. **Refactoring code into multiple functions**: Similar to a table of contents, this allows your
   code to be navigated by looking at the function calls.

## Excessive Organization

Avoid breaking your code into too many small functions. This can lead to excessive jumping around to
read each individual function, similar to writing an essay where every two lines you direct the
reader to "see p. 5" or "see p. 20". This constant navigation reduces comprehension.

Instead, organize your code into medium-sized pieces, much like structuring an essay into coherent
sections rather than tiny fragments.

## See Also

-   [Cyclomatic Complexity](../measurements/cyclomatic_complexity.md)

DSG 2024-06-19
