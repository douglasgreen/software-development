# Clean Code

Here's some criticisms of clean code principles that I don't like. They are quoted from the
[Summary of 'Clean Code' by Robert C. Martin](https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29).

## Specific criticisms

> Prefer polymorphism to if/else or switch/case.

This principle is an example of what I like to call escalation. It's where you reject a simple
construct and use a more powerful construct instead. If statements are not good enough so you use
functions. Functions are not good enough so use classes. And soon your code is littered with useless
classes that could have just been if statements.

There are several problems with this principle:

1. It fails to specify conditions when polymorphism is preferred. You shouldn't just arbitrarily
   prefer one thing over another without looking at context.
2. It fails to respect the semantics of polymorphism. Polymorphism is supposed to be used when a
   class type varies in its implementation.
3. Code that was localized in one if or switch statement is now broken apart into multiple functions
   that you have to search for.

So in conclusion you should prefer polymorphism when making decisions about type. But when you're
just making decisions about values, use if and switch statements.

> Use dependency injection.

This principle is also presented as an absolute. Whether or not you should use dependency injection
should be a decision that you make that respects context. Dependency injection is useful when:

-   You might want to configure the object you are injecting different ways.
-   You might need to mock the object you're injecting for unit tests.

Classes that don't need different configuration and don't need to be mocked are often simple enough
to construct inside another class. This avoids cluttering up your dependency injection framework
with every little class.

> Prefer dedicated value objects to primitive type.

This is another case of escalation and of arbitrary preferences. You should decide between things
based on their definition and the context. Otherwise your code will end up full of boilerplate and
overused techniques.

Objects should be used when your data value has complex parts, special functions, or requires
validation. An example would be a URL. It could be passed around as a string but that doesn't make
it easy to extract the parts of the URL or determine if it's valid.

It can also be passed around as an instance of the URL class which improves type hinting. Strings
can be confused for each other but different classes cannot.

> Functions [should be] small [and] do one thing.

Clean code says that functions should be no more than 10-20 lines of code. A different book, Code
Complete by Steve McConnel, says that function should be no more than 100 or 200 line codes. The
difference is that clean code was based on the author's personal preferences whereas code complete
was based on research of working programmers. The research says that the longer functions are less
costly to develop and typically have no more bug density than the shorter functions.

So function length is not really a good measure of quality. I measured a general PHP code base and
found that 99% of the functions were less than 150 lines of code already. So function size is
something you only have to worry about in rare cases.

Function name should also be shorter than what they said in the clean code book. The Clean code book
gives absurd examples of two line functions that are excessively split apart and fragmented. This
creates the cost that you have to jump around to read the code rather than just reading it in
sequence. It also means as function names are too long because they are too many of them. He uses
function names to substitute for comments so he has a really long function name instead of a
comment.

In general, names are not descriptions but rather simple handles. So shorter names are preferred.

> Don't use flag arguments. Split method into several independent methods that can be called from
> the client without the flag.

This rule doesn't scale. It works OK if you have a function that has only one flag. You can provide
two different function names instead. If you have a function with five flags, you would have to
provide 2^5 = 32 function names in order to encapsulate all of the possible combinations of flags.
Clearly this will not work.

> Always try to explain yourself in code.

Code can't explain why it does things so it is not a general substitute for comments.

> Prefer non-static methods to static methods.

Static methods are fine if they don't manipulate static variables. It is surprising to me that
people fail to distinguish between these two things. Static methods are easy to unit test if they
are pure functionality and require no setup. That is the functional paradigm.

> One assert per test.

That sounds nice but now you have too many functions in your test class again. I don't see why I
would have trouble tracking down an assert statement to a particular line of a function even if
there's more than one of them.

## General conclusions

The problems with Clean Code are:

-   It is based on the author's personal preferences.
-   It ignores research of actual working programmers.
-   Its advice is sometimes poorly expressed and ignores context.
-   Its advice doesn't scale beyond toy examples.
-   It ignores side effects such as program fragmentation.
-   It ignores program performance.
-   It provides at best weak indicators of code quality.

I personally get better results from linters that check for specific bugs than general clean code
considerations.

In conclusion, don't assume that Clean Code always gives good advice and don't follow it blindly.
Your efforts to clean up your code should mainly focus on the meaning of the code and not on
superficial syntactic manipulation. Ultimately, clean code is readable and meaningful code. Your code
will be clean when you spend time to clean up its first draft quality and think carefully about the
best ways to organize and express it. It also becomes clean through unit testing and widespread
application by actual users who find its flaws. There isn't any shortcut to clean code.
