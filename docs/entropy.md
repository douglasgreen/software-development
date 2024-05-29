# Entropy

## Programming languages

Programming languages have bad entropy. The problems are:

-   Their design mainly consists of lower level syntactic features.
-   Those features get written into millions of lines of code.
-   The code depends not only the feature details but also on their
    implementation.
-   As lower level features, they are difficult to version, that is, to import
    different implementations.
-   The language is often designed as a pile of features. More features are
    constantly added to the pile, yielding ever-increasing complexity.
-   Every feature in isolation looks good because it's presented with some
    trivial use case that it solves. The overall cost of complexity is not
    considered.
-   The features were not considered in the original design so they are poorly
    integrated.
-   In programming languages, new features are often introduced with punctuation
    marks, leading to overloaded and unreadable series of punctuation marks.

The result of these design constraints is that programming languages tend to
degrade strongly over time.
