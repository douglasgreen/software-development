# Miscellaneous

## Levels and modularity

Organizing requires you to break things down into a small number of levels. Each level should
consist of a medium number of modules, arranged in a hierarchy. If you just have one module then you
don't have to break it apart, just like you don't need a subdirectory if you just have one file.

## Rationality versus rationalization

Rationality means objective thinking produces valid facts and use a sound reasoning to explicitly
reach conclusions. Rationalization is a week form of rationality that often is a substitute. With
rationalization, you start out with a predetermined conclusion and present fake reasons for it
without freely considering alternatives.

## Teamwork

The unit of productivity and software development is the team, not the individual. The most
productive team is not necessarily composed of the smartest individuals as Google studies have
shown. Rather it consists of people who work together constructively and communicate equally.

Adam Smith showed in Wealth of Nations that a team producing pins by assigning people specialized
roles is much more productive than single individuals trying to produce their own pins. This is the
principle of specialization and it is powerful. This principle should also be applied at software
development by assigning specified roles to team members. For example, one person can't design the
database, one person can design the API, one person can't implement the API, one person can consider
network issues, one person can do debugging, etc.

## Golden mean

Don't do too little or too much of anything. So don't do extreme programming that tries to turn
everything up to 11. And don't do pair programming unless you're training someone.

## Agile

Agile was designed by programmers and it shows. They take the things that programmers find boring
like writing documentation, doing design, or attending meetings and they say not to do too much of
them. That's like saying not to eat too much vegetables or brush your teeth too much. If you just
avoid doing those things all together you're still following their advice.

Better advice would follow the golden mean. They would say to not do too little or too much of those
things.

Test driven development does not compensate for a lack of design. They have different goals. Design
is trying to answer what you're supposed to be doing and test driven development just tries to make
sure you're doing it correctly. TDD is no substitute for a lack of design.

## Design up front

Doing enough design up front makes your project twice as likely to succeed. The design should be
conceptual and make your project easy to describe and understand.

## Fallacy of simplifying the part

There is a widespread fallacy and programming that if you simplify the part you simplify the whole.

An example is measuring the complexity inside of a function but not measuring the complexity of
functions. The inevitable conclusion is that you should break your code into more functions. This
doesn't actually make your code simpler. Breaking your code into functions means you have to skip
around to find all of the functions and read them. That's like reading a book where every other line
says see page 103 or see introduction. You spend more time skipping around than you do reading. That
is not simpler.

Another example is breaking all your code into microservices. The same code is there so it is not
simpler. But now your code has to be taken to account of being transported across the network, which
is more complicated and less reliable.
