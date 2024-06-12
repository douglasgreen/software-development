# JavaScript

Here are my JavaScript notes.

## Data model

The DOM looks like a shared data and rendered HTML model all mixed together. Wouldn't it be better
if the data model was defined as a separate layer? And an event queue on top of that? So data and
its updates could be managed in an orderly fashion. This should respect the modularity of the page
as independent widgets, meaning each one might have its own data model and event queue.

A set of widget tags like .menuBar could create a data object menuBar that holds their shared data
model.
