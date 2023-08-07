# To-do list

* Capitalize headings

## Software engineering

The way software engineering is typically described it doesn't specify enough constraints to ensure good solutions. It's like they're saying, "do whatever you want, just draw pretty pictures about it".

Programming is part psychology and part applied math. The psychology part is hard to measure and hasn't been studied enough. The difficulty is that people can adapt to any sort of methodology. So the methodology can seem to be productive without actually being better than other methodologies. This makes it difficult to tell when there's actual improvements to be made.

There's also a lack of concrete feedback because everything works, even bad design. Programming is brittle and encourages focusing on overly fine details, because getting them wrong might break the program. This has a tendency to cause programmers to lose sight of the forest for the trees. They focus on micro optimization and lose sight of the big picture.

Software engineering is also made more difficult by constantly changing standards and developer fads. This makes good engineering and moving target. Every time a new language comes out, we have to reinvent the wheel. But the old systems suffer from entropy so badly due to lack of versioning, new system become inevitable.

## Programming myths

More smaller parts are better -  too much complexity. Combine this with other text.

More tools are better. -  too much dependencies and harder to upgrade.

## jQuery

JQuery is hard to upgrade because libraries depend on other libraries. These are often just installed by linking them all to the whole program. So there is nothing to tell you where the dependencies or jQuery are being used. The entire program must therefore be upgraded as a whole. Because neither jQuery nor nor the libraries that depend on it provide back compatibility, the result is frequent major front end breakage.

## Premature optimization

This means you shouldn't obscure your program to make optimizations that you probably won't need. But rather you should wait until optimization is needed. The trade-off here is between programmer time who has to read obscure code and computer time, especially where very little computer time is being saved.
