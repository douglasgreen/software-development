# Lisp

There are two basic families of Lisp:

-   Common Lisp, the overcomplicated language derived from the Lisp industry.
-   Scheme, the oversimplified language derived from Academia.

Common Lisp has a thousand-page manual. It was designed by combining a
hodgepodge of different offerings from different vendors. Nobody compromised so
they threw in everything but the kitchen sink. This is especially absurd because
Lisp is supposed to be an extensible language. Compare that to C which requires
you to import a header to even use the print statement. C has a more modular
design.

Scheme is oversimplified and doesn't bother to provide useful libraries. It's
standards are also bogged down in perfectionism and are starting to reach the
complexity of Common Lisp.

## Too many parentheses

Lisp has too many parentheses. The parentheses are used in expressions
(small-scale) and as markers for function blocks (large-scale). Because there is
no distinction between the small-scale and large-scale features of your program,
it is harder to read. C uses parentheses for small-scale features and braces for
large-scale features.

## Too many function calls

Lisp uses a functional paradigm rather than an imperative paradigm. This leads
to too many nested function calls. Operations A, B, C, and D are nested like
`D(C(B(A)))` so you have to read them inside out. This is made worse by the fact
that functions have multiple arguments so it's hard to find the beginning and
end of function calls.

Imperative languages are more readable because they put statements in the order
of execution:

```
A;
B;
C;
D;
```
