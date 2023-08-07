# Iterative Design and Incremental Development

Iteration means repeating and incrementing means increasing.

So iterative design means going through repeated cycles of design improvement based on feedback from the prior release.

And incremental design means building a base working system, then going through repeated cycles of adding to it in increments.

As an example, consider publishing a book. There are three basic models of publishing a book.

1. The book is published once and for all and never changed. This model is used by most works of fiction.
2. The book is published but based on feedback from the readers it improved in subsequent editions. This model is used by many textbooks.
3. The book is published in some minimum form. Then it is republished multiple times with additional material each time. This model is similar to the second model but this model is put into production faster to get earlier feedback.

Software is usually designed in the second or third model. In the second model, feedback from users is used to improve the software after it is released in full. The reason this model works is because releasing the software to production gets feedback from actual users. The users have a diverse variety of requirements and work under a variety of conditions. Their feedback helps expose errors and suggest improvements. It is also easier to provide feedback on a finished product then on a conceptual product.

The third model is the best model for software though. This model is conceived of in a layered or incremental design. The minimum viable product, or core of the system, is released to get it into the hands of users as quickly as possible. Then there is a planned series of improvements and feature additions. Each improvement or feature is finished and released as soon as it is ready. The benefits of this model include:
* The software is up and running more quickly with its most important features. This minimizes the delay in which the important features get into the hands of the user.
* Releasing the product in layers or stages encourages a modular design where components are properly separated. This helps prevent a problem of a system that is not properly separated into components, called a "big ball of mud".
* The system is operational at each stage so it never strays too far from a working system. This minimizes the chance of project failure of having to integrate too many changes at the same time.
