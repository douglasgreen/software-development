# Easy Is Bad

In the world of design, easy is bad. Some popular languages are designed to make it easy for people
to get started. But that usually means a lack of structure and bad design.

For example CSS wanted to make it really easy to add their styles to HTML. So they let you select
just about anything, including basic tags or the \* to select everything. There is no modularity or
structure of any kind though so it doesn't scale. And all of the implicit styling gets applied when
you don't want it to and haven't asked for it.

PHP wanted to make it easy to get started as a templating language. So the variable names all start
with $ and everything went in the global namespace with no structure. These are exactly the
handicaps of the language today. Namespaces, classes, and auto loading were added later but they
have to do with all of the legacy code.

On the other hand, Java started out with an object-oriented structure. People complain that just to
write hello world you had to create a class so it was not easy. But it's ubiquitous structure makes
it easier to scale programs.

Just taking the easy way and dumping code in a pile with no structure makes it seem easy to get
started. But that is a bad design and makes it harder to finish.

So as a designer, consider making structure mandatory and taking the not easy road.
