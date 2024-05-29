# Criticisms of Popular Web Technologies

## Criticisms of CSS

CSS, with its peculiar specificity rules, operates on a system that assigns
scores to different types of selectors:

-   !important = top priority
-   Inline styles = 1000 points
-   IDs = 100 points
-   Classes = 10 points
-   Tags = 1 point

However, this system seems counterintuitive and problematic for two main
reasons.

1. IDs are often assigned to high-level page elements, while classes are
   typically linked to lower-level elements. This hierarchy complicates the
   process of overwriting global styles with more specific, widget-level styles.
2. The current design makes coordination between third-party stylesheets more
   challenging. The absence of a well-defined system for establishing precedence
   among stylesheets, apart from manipulating individual style weights, further
   complicates matters.

A more efficient design for CSS would rely on simple precedence rules rather
than weight-based specificity. That is, the most recently applied selector would
always take priority. Implementing such a change could address the two design
issues mentioned earlier:

1. It would allow for the semantic application of IDs or classes, eliminating
   concerns about their specificity weights and the need for later overwrites.
   Therefore, IDs could naturally be used for top-level page containers, with
   the ability to be overridden by lower-level page classes.
2. The precedence of third-party stylesheets would be determined by the order in
   which they were applied, enabling more streamlined coordination.

In the absence of a well-designed CSS system, a practical solution would be to
stick exclusively to top-level class-based selectors applied to widgets. By
avoiding the use of !important and ID-based selectors, most problems can be
mitigated, given that all selectors would then operate at the same level of
specificity. And within each widget:

-   Tags can be used as selectors inside the top-level class selector of the
    widget without affecting unrelated usage of the tags in other widgets.
-   Inline styles can be used because they are always applied last so they don't
    violate the precedence rule.
-   Information hiding and code brevity are achieved because the widget class
    can apply complex substyles without needing to specify their subclass names.

## Criticisms of JavaScript

JavaScript is a programming language that was hastily put together and gradually
refined over years via a committee-led process. Its fundamental design leaves
much to be desired, marked by issues such as:

-   **Output Dependency Issues**: Operations functioning at the output layer,
    leading to browser inconsistencies and fragility due to an over-reliance on
    specific document formats instead of managing data in a more universal
    manner.
-   **Error Handling Deficiencies**: Subpar error handling and reporting which
    operates at the user level rather than at the server level.
-   **Race Condition Challenges**: Race conditions brought on by an inadequately
    designed event model tied to element rendering.
-   **Dependency Stack Complications**: Excessive rotation, bloat, and intricacy
    within the dependency stack.
-   **Language Misfeatures**: Various other language shortcomings outlined in
    the book 'JavaScript: The Good Parts'.

Furthermore, it also shares a common problem with CSS - the lack of an effective
organization system, albeit without the specificity hierarchy. To my knowledge,
none of the visual designers who laid down the CSS standards examined here took
any initiative to develop similar JavaScript standards. Nevertheless, PageMaker
addresses this organizational deficit with the widget system, co-organizing CSS
and JavaScript into widgets. Be aware that this system doesn't inherently
resolve any of the problems listed above. Therefore, it is advised to restrict
the use of JavaScript to specific page animation requirements that don't involve
reloading the page.

Future iterations of PageMaker may attempt to rectify some of these issues with:

-   **Output Dependency Issues**: Systematized data retrieval methods to
    eliminate the need for excessive data encoding within the page.
-   **Error Handling Deficiencies**: Refined error handling mechanisms that log
    errors server-side for developer examination.
-   **Race Condition Challenges**: The introduction of an event queuing system
    for each widget to prevent race conditions and facilitate cooperative
    development of event handlers.
-   **Dependency Stack Complications**: Minimization of JavaScript dependencies
    by formulating simple, ad hoc alternatives.
-   **Language Misfeatures**: Formulation or adoption of a simplistic JavaScript
    style guideline to sidestep language misfeatures.

### @todo Combine this

JavaScript is widely used as a component and page builder nowadays. I don't like
it though and I don't like the JavaScript ecosystem.

-   JavaScript is architecturally poor because it starts on the output layer
    with accidental details about how the document is presented.
-   JavaScript runs in the browser which leads to poor error reporting and
    browser incompatibilities.
-   JavaScript always drags in a giant pile of dependencies to maintain.
-   Typical JavaScript is lacking in the features of well-designed modularity
    and typing that enable scalable, well-organized programming.
-   The JavaScript language itself was hastily designed and polished by
    committee. It's endless feature enhancements make it more complex without
    making it more attractive. It's the only language I know that has a book
    that describes the good parts and all of the bad parts that you should
    avoid.

My basic concept of JavaScript is that it should be used to update the page but
not to render the page. Thus I use it only where local page updates are
required. The initial page load should always be pure PHP. This also implies
that I avoid depending on REST APIs for basic page rendering so that page loads
are monolithic and fast.

## Criticisms of single-page apps

While single-page applications (SPAs) can offer a smooth and responsive user
experience, they are not always the optimal solution. Trying to mold all
applications into this design paradigm can inadvertently forego the benefits of
stateless page loads, mirroring the convoluted process of cramming your entire
codebase into a god object.

One of the core principles of SPAs, the absence of page refreshes, essentially
leads to an aggregation of all your JavaScript into a bulky, cumbersome entity.
Moreover, it perpetuates the global state of your application in JavaScript over
the entire runtime of your web app, adding layers of complexity to your
application design.

PageMaker, on the other hand, advocates for the disintegration of your
application into distinct, intuitively structured pages. These pages can be
navigated via a menu or a state machine, providing a user navigation experience
that is both clear and efficient. The majority of the page rendering should be
undertaken using direct database queries and PHP templating, reserving
JavaScript for on-page animations and utilizing a limited local state that
refreshes upon every page load. This approach results in a more organized and
manageable application design, keeping complexity in check.

## Criticisms of REST APIs

REST APIs are often misused, employed as a code organization tool when in
reality, they're intended as units of network architecture. Microservices are
even worse because they break down services into granular units that are too
small.

In the past, it was common to build unstructured PHP monoliths. Over time, these
were swapped out in favor of REST APIs. However, a better approach would have
been to use namespaces and autoloading, a pair of advanced structural tools
provided in newer versions of PHP.

Before deciding to use REST APIs, it's crucial to weigh their advantages and
disadvantages.

The **benefits** of REST APIs include:

-   **Language Compatibility:** They can be called by a variety of programming
    languages.
-   **Dynamic Page Interaction:** They can be employed for interactive page
    features without necessitating a page reload.
-   **Server Load Distribution:** If your server is at capacity, REST APIs can
    be used to divide services between multiple servers.

However, the **drawbacks** of REST APIs shouldn't be overlooked:

-   **Performance:** REST APIs operate slower than direct database access.
-   **Code Overhead:** They require additional layers of code for their
    production and consumption.
-   **Network Delays and Reliability:** Network delays and reliability issues
    are introduced.
-   **Data Fragmentation:** Your databases can become unnecessarily divided
    between different servers and APIs.

These drawbacks can be significant, leading to situations where avoiding a REST
API could be more beneficial. You might not need a REST API if:

-   **Single Server-side Language Use:** You are only using one server-side
    programming language, such as PHP.
-   **Modular Structure:** Your objective is to grant your application a modular
    structure, which can be achieved using namespaces and autoloading.
-   **Versioning:** Your need is for versioning, which can be realized with
    Composer versioning or content versioning.
-   **Database Lookup:** If your requirement is merely a database lookup for
    some associated value, a direct SQL join would suffice.
-   **Database Capacity:** If your database is at its limit, the solution is to
    utilize multiple database hosts rather than multiple service hosts.

## Criticisms of virtual machines

The prevalent trend of employing virtual machines (VMs) in modern development
deserves thoughtful examination. Both the overuse of VMs and REST APIs seem to
stem from a flawed understanding: the belief that dissecting an architecture
into smaller parts automatically simplifies it. This, however, isn't necessarily
true.

A well-designed system should be easy to explain, understand, and modify. To
demonstrate, let's contrast two types of system: a shared development server and
a group of VMs. Here, we'll assume that the shared server was initially
established by the Networking Department and subsequently replaced by VMs. These
VMs are running 10 unique projects for 10 different developers, coordinated by
DevOps, with individual developers also establishing their own VMs.

-   **Shared Development Server:** This system is relatively straightforward to
    describe, likely running a single PHP version and one or multiple versions
    of Node, jQuery, or related libraries. Its configuration includes a single
    host and a database server. This simplicity in description and maintenance
    is a key advantage. The Networking Department, rather than developers,
    generally oversees it, adhering to the principle of specialization.
-   **Virtual Machines (VMs):** In contrast, VMs are more complex to describe.
    Given that the 10 developers could each check out multiple VMs, there could
    be hundreds of unique VM configurations. Each one possesses its own PHP,
    Node, and jQuery version, requiring intricate coordination for the setup and
    configuration of these distinct environments. Additionally, each developer
    has to manage the setup, operation, and troubleshooting of these VMs—a task
    previously undertaken by specialists.

The shift to VMs often leads to a scenario where each individual part is less
complex, but the overall system becomes much more intricate.

Similarly, REST APIs have the same issue. Segmenting code into separate REST
APIs may make the APIs appear simpler. Yet, to fully describe them, you must
also account for access credentials, the layers producing and consuming the API,
and the network's condition. This results in a system that, while comprised of
simpler components, becomes more complex and brittle in its entirety. Dividing
the complexity of a whole project into separate parts doesn't eliminate
complexity; it can actually enhance it.

Generally, it's likely preferable to begin with an organized monolithic
architecture on shared development server, only opting to segment the design for
specific reasons, such as exceeding the capacity of a single server.

<!-- DSG/ChatGPT 7/25/2023 -->
