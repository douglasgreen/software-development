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
