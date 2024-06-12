# Cyclomatic Complexity

Here is a summary of how cyclomatic complexity is calculated for switch/case statements:

-   Original McCabe Cyclomatic Complexity: Each case statement adds 1 to the complexity.
-   Modified Cyclomatic Complexity: The switch statement itself adds 1 to the complexity, and case
    statements do not add to the complexity.

The calculation also adds 1 for every if and while statement. This is wrong because:

-   It treats independent if statements as equal to dependent ones.
-   It treats if statements that return from a function as equal to those that remain.
-   It treats case statements as equal to switch even though they only depend on a value not
    different conditions and usually don't fall through.

In comparison:

-   3 if statements that depend on each other have 8 outcomes that are intertwined.
-   3 if statements that are independent have 8 independent outcomes.
-   3 if statements that return cut short some of the outcomes.
-   3 case statements have only 3 possible outcomes.

## Switch vs. if

Switch statements are one test with n outcomes (the cases). If statements are n tests. They are not
the same.

For example, 10 if statements have 2^10 = 1024 possible outcomes. But a switch statement with 10
cases (assuming no fallthrough) has 10 possible outcomes. Counting each as equally complex is wrong.

## Function boundaries

Splitting if statements into functions doesn't make them simpler per se.

Imagine that I have a single function with 10 if statements. It offers 2^10 = 1024 possible
outcomes. Now imagine that I split it into two functions with five statements each. Each function
seems simpler because it only offers 2^5 = 32 possible outcomes. But the first function is called
followed by the second function, which means that including the functions in your consideration we
have 2^5 _ 2^5 = 32 _ 32 = 1024 possible outcomes.

This is shuffling the code around and not reducing its complexity. It only seems to be reducing its
complexity because our measure calculates the measure within the function but not the measure
between functions. This is a defect of the measurement and shows that it is not helpful.

## Essential vs. accidental complexity

Essential complexity is the part of the problem that can't be reduced. If you have 10 if statements
or 10 cases, then that is an essential part of the problem and you can't reduce the complexity.
Splitting them into new functions doesn't simplify it because the same 10 if statements in it or
same 10 cases are still there.

Accidental complexity is the part of the problem that can be reduced. That is the part you should
focus on. An example of accidental complexity is when you include two different purposes within the
same function. Splitting them between two different functions simplifies it because now each
function serves one purpose.

## How to reduce complexity

In order to reduce complexity, we must operate on a semantic level not merely on a syntactic level.
Complexity is the level of detail of the system and how it is described or modeled in your mind. In
order to reduce this complexity, we organize things into meaningful categories.

An example is making breakfast. It might consist of a 20 different steps. So to describe it you
would have to describe all 20 steps because they are unrelated and unorganized. To organize it
better we would break the steps down to the categories, such as: gathering the ingredients,
preparing the ingredients, cooking the ingredients, serving the food, and clean up. Now that the
task has been broken into meaningful categories it has better organization and is easier to describe
and understand.

Another example is putting things into boxes. If you have a hundred items they are hard to describe
because they are not organized. If you simply start following a low-level rule like put no more than
10 items into one box, you can put your 100 items into 10 boxes. But they are still hard to describe
and understand. The way to organize is to group meaningfully related items into boxes that are easy
to describe. For example, toys go in one box, tools go in another box, books go in another box, etc.
Now the system consists of a medium number of elements and is easier to describe and understand.

Code is the same way. We look for unrelated sections of code that can be separated into a box (a
function) and given a meaningful label. That makes your program easier to understand as a series of
function calls. This is done by meaning and not by arbitrary units of code size. The underlying
essential complexity in unchanged, but it is still easier to understand because it is grouped into
meaningfully related boxes.

## Conclusion

The complexity measures are probably redundant to simple measures of lines of code. And the measures
of lines of code should be used as a general guideline when to consider refactoring, not as a hard
rule. Remember that merely splitting code into separate functions doesn't reduce its complexity. It
is the act of giving those functions a single purpose and a meaningful label that is what reduces
the complexity.
