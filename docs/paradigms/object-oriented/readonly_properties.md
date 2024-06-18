# Readonly Properties

There are three kinds of properties in PHP: const, readonly, and variable.

Const properties are the simplest. They are always initialized when defined and cannot be changed.
But they are limited because they have to be defined at compile time.

Readonly properties are the next simplest and should be preferred when possible. Readonly properties
should be initialized in the constructor by direct assignment rather than by using setters. That
makes it easy to determine how they are initialized. It also sends a signal that these properties
won't change.

Variable properties can be set at any time and changed at any time, therefore they are the least
preferred alternative.
