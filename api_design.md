# API design

## User-Centered API design

> Before we take a look at the actual Event Tracing for Windows API, I want to walk the walk here and do exactly what I said to do in last week’s lecture: write the usage code first. Whenever you evaluate an API, or create a new one, you must always, always, ALWAYS start by writing some code as if you were a user trying to do the thing that the API is supposed to do. This is the only way to get a nice, clean perspective on how the API would work if it had no constraints on it whatsoever. If it was “magical”, as it were. And then, once you have that, you can move forward and start thinking about the practical problems, and what the best way is for you to get to something implementable. [The Worst API Ever Made, by Casey Muratori](https://caseymuratori.com/blog_0025)

The quote emphasizes the importance of user-centered design when creating or evaluating an API (Application Programming Interface). Let's break down the quote and its significance for good API design.

**"Write the usage code first."**

This phrase is foundational. It means that before an API designer even begins constructing the actual API, they should write sample code that demonstrates how a user (typically a developer) would use the API to accomplish specific tasks. By doing this, the designer gets a firsthand feel for the user experience. This code is not about implementing the API's functionalities but simulating its expected behavior from the user's perspective.

**"Whenever you evaluate an API, or create a new one, you must always, always, ALWAYS start by writing some code as if you were a user trying to do the thing that the API is supposed to do."**

When an API designer puts themselves in the user's shoes, they're better equipped to predict challenges or friction points users might face. By writing "usage code" or "pseudo code" for expected tasks, the designer can identify gaps, redundancies, or complexities in the proposed API design.

**"This is the only way to get a nice, clean perspective on how the API would work if it had no constraints on it whatsoever."**

By imagining a perfect, constraint-free environment, designers can visualize the most user-friendly and intuitive version of the API. This "ideal state" can serve as a benchmark for the actual design.

**"If it was 'magical', as it were."**

The word "magical" here suggests an API that works seamlessly, where everything feels intuitive and natural for the user. It embodies the principle of simplicity and ease of use.

**"And then, once you have that, you can move forward and start thinking about the practical problems, and what the best way is for you to get to something implementable."**

After designing this ideal or "magical" API experience, the designer can then grapple with the real-world constraints (like technical limitations, legacy systems, or budget considerations) to make the API practical and implementable. Balancing the "ideal" with the "practical" often leads to a more thoughtful and effective API design.

**How are use cases and user stories relevant?**

1. **User-Centered Design:** Both use cases and user stories place emphasis on the user's needs and requirements. An API that doesn't address its user's needs will likely not be adopted or will be frustrating to work with.
2. **Clarification of Functionality:** Use cases and user stories help in clarifying what exactly the API is supposed to achieve. They provide a narrative of how the end user (developer or system) will interact with the API.
3. **Feedback and Iteration:** As designers write user stories and visualize use cases, they can gather feedback from potential users, making iterative improvements to ensure the API's design remains aligned with user needs.
4. **Simplicity and Intuitiveness:** Through user stories, designers can focus on the essential functionalities and avoid unnecessary complexities. A good API should allow users to achieve their goals without needless hurdles.

In summary, the quote emphasizes the importance of starting from the user's perspective when designing or evaluating an API. By visualizing the ideal user experience first and then reconciling it with real-world constraints, designers can ensure their API is both user-friendly and practical. Use cases and user stories serve as tools to maintain a user-centric approach throughout the design process.

<!-- DSG/ChatGPT 8/1/2023 -->
