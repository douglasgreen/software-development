# Critical Thinking for Programmers

## Defining critical thinking

Critical thinking in the realm of programming means evaluating and understanding the "why" and "how" behind your methods, ensuring that they're the most effective means to address a problem.

Lacking critical thinking, you might fall into:

1. **Magical Thinking**: Believing that a particular technology or method will solve all challenges without understanding its nuances.
2. **Cargo Cult Programming**: Blindly copying technical methods from others without understanding their purpose or context.
3. **Jumping on the Bandwagon**: Abandoning older technologies just for the sake of using newer ones, without evaluating their actual benefits.

## Enhancing your critical thinking skills

To practice critical thinking:

1. Understand your problem's context. What value does your work bring? How does it differentiate from others?
2. Evaluate the technologies or methodologies applicable to your situation. Ask:
   * Why is this technology or method beneficial?
   * When is it most suitable?
   * When should it be avoided?
   * How can I best employ it, and what best practices should I follow?

Avoid pitfalls like:

* Adopting technologies simply because they're popular.
* Not justifying the use of a particular technology for your specific context.
* Over-relying on a single technology without considering its limitations.
* Not having clear guidelines for using a technology effectively.

For instance, the trend of using REST APIs everywhere can be counterproductive. While beneficial for large-scale businesses or multi-language support, they might introduce unnecessary complexity for smaller projects. Instead of adopting it blindly, critically evaluate its use-cases:

* **Benefits of REST API**: Scalability across multiple hosts, partial page updates, support for multiple languages.
* **Ideal Use-Cases**: Services outgrowing servers, partial page refreshes, multi-language support.
* **Limitations**: Overhead for simpler projects, potential for reduced performance, and possible data fragmentation.
* **Best Practices**: Establish clear conventions and guidelines, considering alternatives and specifying when it's best utilized.

Rather than relying solely on REST APIs for modularity, consider simpler solutions like separate code projects, namespaces, or database tables.

## The boundaries of critical thinking

While critical thinking is vital, it's not a panacea. Relying solely on philosophical generalities can sometimes be counterproductive. Along with critical thinking, successful project development requires:

* Strong business acumen.
* Robust technical engineering skills.

Remember, every tool, including critical thinking, has its place. Knowing when and how to use each tool effectively is the hallmark of a seasoned programmer.

<!-- DSG/ChatGPT 7/25/2023 -->
