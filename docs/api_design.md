# API design

An API is an application program interface. That means it is an interface for programs to use rather
than a user interface. There are two kinds of APIs.

-   Program APIs, in which you design a library interface for function calls in a programming
    language. Examples include the Microsoft Windows API or the Java class library API.
-   Network APIs, in which you design a network interface for remote function calls in multiple
    programming languages. REST APIs are an example of network APIs.

The program API might be in the same repository or a different repository. Storing it in a different
repository allows for clean project separation while still avoiding network delays at runtime.

The basic facts of APIs are:

-   The structure of an API should map directly to its functionality.
-   API labels should be understandable by reflecting their purpose.
-   An API should offer complete functionality for the user by anticipating their needs.
-   Users write complex software that depends on the API so it should maintain backwards
    compatibility.
-   Network APIs conveniently offer services over the internet but that introduces delay and
    scalability issues.
-   Network APIs convert all data to string and back again, which may cause data typing issues.

## User-Centered API design

To design a good API, you should think of the user of the API. Write a list of user stories about
how the functions of the API will be called. Then break down the user stories into use cases that
show individual examples of the API being used.

When you break down a task like API function calls down into steps, the purpose is that the user can
omit or customize each step. If the user doesn't need to emit or customize a step, it should
probably be omitted from the API as an internal implementation detail. Otherwise your API has
redundant and unnecessary steps that never vary. This is boilerplate that increases the size of the
API usage without increasing its functionality or flexibility.

## Versioning

API design isn't just about crafting an interface to meet current user needs; it's also about
considering the future evolution of the system. While user-centered design emphasizes a fresh and
focused approach, the practical reality of API design is that it must adapt and grow, often
necessitating backward compatibility with previous versions.

### **Why Versioning Matters in API Design**

Unlike a blank slate where everything can be structured precisely as desired, an existing API must
evolve in a manner that accommodates both new and existing users. This poses a unique set of
challenges:

1. **Complexity of Backward Compatibility:** Ensuring that new features and changes do not break
   existing implementations can lead to an unwieldy and less coherent design.
2. **Balancing Innovation and Stability:** Introducing novel functionalities while maintaining
   stability for existing users requires careful planning and execution.

### **A Systematic Approach to Versioning**

To address these challenges, a well-structured system of versioning is not just beneficial but
essential. Versioning:

-   **Enables Upgrades with a Planned Strategy:** By defining different versions, you can introduce
    changes, deprecate old features, and optimize the system in a controlled manner. Clients can
    choose when and how to migrate to the new version, easing the transition.
-   **Allows Multiple Versions to be Used Side by Side:** Different versions can coexist, allowing
    users to work with the version that best suits their needs. This parallel availability ensures
    that new improvements don't alienate existing clients while still providing a pathway for growth
    and development.

### **Conclusion**

Versioning is more than a technical solution; it's a strategic approach to API design that
recognizes the dynamic nature of software. By adopting a well-managed system of versioning, you
create an adaptable API that can innovate without sacrificing reliability and compatibility. Whether
you're extending existing functionalities or embarking on substantial changes, versioning provides
the framework to do so in a user-friendly and sustainable way.

## Mistakes

1. Using network API when program API would be better

2. Poorly Defined Contracts

A well-defined API contract is essential. It sets the rules for how the API should be used,
including available data formats, methods, and endpoints. A poorly defined contract can lead to
misunderstandings, bugs, and unexpected behavior. To avoid this, consider using the OpenAPI
Specification to document the API. This standard allows developers to clearly define the structure,
endpoints, methods, and data types used in their APIs levelup.

3. Not Considering the Client

The primary design principle of an API should be to maximize developer productivity and promote
adoption. An API should be able to effectively serve the client's needs. One common mistake is
trying to describe all the actions that can be performed on a resource within the resource's
representation, which is not commonly done and can lead to confusion.

4. Overcomplicating the API

Making the API too complex for users can deter them from using it. The API should be strong and
smart enough to perform complex tasks, but simple enough to hide the complexity from the user. To
ensure your API design is simple enough, pretend you are building the whole system from scratch or
ask a trusted customer to test it and report their results.

Don't add API endpoints just in case they might be used. Limit endpoints to necessary support.

5. Inappropriate Error Handling

When no HTTP response code is a good fit or is not fine-grained enough for specific error
conditions, you should pick the closest fit HTTP response and return a body with more information.
This helps the client understand what went wrong and how to fix it.

6. Ignoring Versioning

Not providing versioning info for your API can lead to issues. The client should be able to check
both at compile time and runtime what version of your API is integrated into their system. If such
information is lacking, they’ll not be able to take effective updates/patches.

7. Neglecting Documentation

API documentation is a critical part of the development process, yet it is often overlooked or given
minimal attention. Skimping on documentation can lead to confusion, frustration, and more
troubleshooting on the development side.

8. Not Understanding the Problem to be Solved

Another common mistake is not fully understanding the problem that needs to be solved before
beginning to build a REST API. This leads to a number of issues, such as building an API that does
not meet the needs of the consumers, or building an API that is unnecessarily complex and difficult
to use.

9. Inconsistency

Name, type, or data structure inconsistency in parameters or return values. This will cause errors
for the user of the API.

10. Redundancy

Multiple endpoints that do the same thing.

11. Poor documentation.

Missing, incorrect, or unhelpful documentation.

12. Incorrectly used API versioning.

Having breaking API changes in the same or a minor version.

13. Needless or excessive changes to backward compatibility.

Can't resist shuffling things around, forcing all clients to do the same.

Remember, designing an API is all about keeping it simple, intuitive, loosely-coupled, and scalable.
By avoiding these common mistakes, you can create an effective and user-friendly API.

## Best practices

Organize the API design around resources: This practice involves focusing on the business entities
that the web API exposes. For example, in an e-commerce system, the primary entities might be
customers and orders. The URIs should be based on nouns (the resource) and not verbs (the operations
on the resource). Use interfaces: An interface in PHP defines a contract for what a class can do,
without saying anything about how the class will do it. A class that implements an interface must
provide an implementation of all the methods of that interface. Interfaces can also have constants.
Follow RESTful API Best Practices: RESTful APIs have become the standard for building scalable,
flexible, and maintainable web services. Utilize appropriate HTTP methods (GET, POST, PUT, DELETE)
for the corresponding actions on resources. Include versioning mechanisms, such as version numbers
in URIs or HTTP headers, to support API changes without breaking existing clients. Implement proper
error handling to provide informative error messages when errors occur. Contract-First Approach:
When designing a great REST API, it's important to have great microservices. The Contract First
approach helps you in designing a great contract before implementing it. Use Nesting on Endpoints to
Show Relationships: Different endpoints can be interlinked, so you should nest them so it's easier
to understand them. For example, in the case of a multi-user blogging platform, different posts
could be written by different authors, so an endpoint such as https://mysite.com/posts/author would
make a valid nesting. Don't Create Side Effects on the API: When creating an API, try not to define
everything in one function as much as possible. If the API sets many flags or does many tasks
simultaneously, it should be split into multiple APIs. Understand the Problems Your API Solves:
Before you can design any solution, you need to know your goal, or at least the issue your design
addresses. Your company, group, or product’s strategy will lead the decisions you make during the
API design phase. Adopt Industry Conventions for Your Interfaces: Your API designs should rely upon
industry conventions as a starting point. You probably don’t need to get creative with security,
data formats, or other decisions. In conclusion, designing an effective API involves careful
planning, understanding the business requirements, and following the best practices of RESTful API
design. It's also crucial to provide comprehensive documentation for your API, including clear
explanations of endpoints, request/response formats, authentication mechanisms, and any specific
requirements.

# REST API Guidelines

## Introduction

REST APIs provide a structured way to interact with web resources. Before diving into the details,
let's clarify when and why one might use them, especially in the context of smaller projects or
in-page animations.

## When to use REST APIs

REST APIs are ideal when:

1. **Partial Page Updates**: You need to update only a part of your web page without reloading the
   entire page. This is particularly relevant for in-page animations or dynamic content updates.
2. **Scalability**: Your project might grow and need to scale beyond a single server.
3. **Multi-language Support**: Your application might be consumed by clients written in various
   programming languages. REST APIs offer a universal interaction protocol.
4. **External Access**: You intend to allow third parties to interact with your application.

## Structuring REST APIs

### Endpoints organization

Endpoints, or the specific URLs of your API where resources can be accessed, can reside within your
main project. This means you don't necessarily need to spin off a separate project for your API.
This integrated approach lets you reuse the existing database connection and the HTTP host.

### Scalability aspects

The term 'scalable' in the context of REST APIs can be viewed in two dimensions:

1. **Throughput**: APIs can manage increased loads when dedicated servers handle them.
2. **Latency**: Each API call requires network data transfer, which introduces some delay. This
   latency becomes more prominent when you break down your application into multiple microservices.

## REST APIs: modularity and costs

Let's understand REST API modularity using PHP as our base:

1. **Direct PHP API**: This is the most straightforward approach where your code is broken down into
   classes, and they're loaded as needed. It's efficient and offers the advantage of direct, fast
   function calls.
2. **Project-based Modularity with Composer**: Similar to the direct approach but the code is
   separated into a different repository. It provides better separation but requires managing
   multiple repositories.
3. **Microservice Approach with REST API**: Here, your project is transformed into an independent
   microservice accessible via a REST API.

**Benefits**:

-   **Isolation**: Your code remains encapsulated, promoting better clarity.
-   **Flexibility**: The code can be executed on a different server or can support multiple
    programming languages.

**Costs**:

-   **Data Fragmentation**: The data might be split across multiple sources, complicating
    relationships like foreign keys.
-   **Setup Overhead**: Additional setup and authentication layers are introduced.
-   **Performance Overheads**: Network data transfer introduces latency, and direct PHP access is
    usually faster than API calls.

### Key considerations

1. **Versioning**: Whether you use direct PHP, Composer, or REST APIs, you always have the
   flexibility to version your application.
2. **Modularity**: REST APIs inherently promote modularity, but remember, modular design can be
   achieved even without network isolation.

## REST API Design Best Practices

API (Application Programming Interface) design is a complex but essential part of modern software
development. It enables smooth communication between different parts of a software system, acting as
a liaison between client and server. Here, we explore key principles and best practices that can
guide a robust and effective API design.

### 1. **Adopt a Design-First Approach**

#### a. **Understanding 'Design First'**

The 'Design First' approach emphasizes planning the API before writing any code. By outlining the
entire architecture, you can mitigate potential issues and streamline the development process.

#### b. **Use Specifications**

Specifications provide a detailed blueprint for the API. Common API specifications include:

-   OpenAPI Specification (OAS)
-   RAML
-   API Blueprint

These define paths, operations, parameters, request bodies, responses, and more, and are
machine-readable, which aids in generating related tools.

### 2. **Embrace Existing Standards and Practices (DRY Principle)**

'Don't Repeat Yourself' (DRY) is a programming principle that applies to API design as well.

#### a. **Research Before Designing**

Before embarking on a new API design, check if a similar API already exists or if existing
architectures and specifications can be leveraged.

#### b. **Use Established Architectures**

Consider using common architectures like REST, WebSocket, SOAP, and GraphQL, depending on your
specific needs.

### 3. **Consider Design Elements**

Designing an API involves various considerations, including:

-   **Scalability:** Ability to handle growing amounts of work
-   **Performance:** Efficiency in processing requests
-   **Versioning:** Ensuring compatibility between different versions
-   **Backward Compatibility:** Legacy support
-   **Error Handling:** Effective communication of errors
-   **Documentation:** Clear and concise documentation for users

Security should also be considered, adhering to standards like REST, GraphQL, or SOAP.

### 4. **Maintain Consistency**

Consistency in common operations is key for a user-friendly API. Ensure uniformity in features like
pagination, search, batch operations, long-running tasks, query requests, localization, and
rate-limiting.

### 5. **Emphasize 'API First' Approach**

An 'API First' approach encourages the creation of an API contract in close collaboration with
stakeholders. Ensuring the contract is well-designed leads to stable and enduring APIs. Changes
should maintain backward compatibility.

### 6. **Incorporate Security from the Start**

Security must be embedded in the design process. Key areas include:

-   Authentication
-   Authorization
-   Access Control
-   Session Management
-   HTTP Headers and CORS
-   Encryption (TLS ciphers)
-   Certificates Management
-   Penetration Testing

### Conclusion

API design is a continually evolving process, with new versions built upon old ones. By following
these best practices, you can create flexible, robust, and efficient APIs that stand the test of
time. Regularly review and iterate on your design to ensure it meets current needs and industry
standards.

## Versioning

As APIs evolve, maintaining backward compatibility becomes essential, often leading to increased
complexity and inconsistencies in design. Over time, the integration of new features alongside
deprecated old ones can result in a disjointed and less coherent API structure.

### **Why Versioning?**

Versioning is the practice of providing different versions of an API to manage these challenges, and
it plays a vital role in maintaining a well-structured and user-friendly API. Here's why versioning
is recommended:

1. **Backward Compatibility:** Older versions of the API can be preserved, allowing existing clients
   to function without modification.
2. **Clean Integration of New Features:** New versions can introduce improvements, optimizations,
   and new features without being constrained by legacy design choices.
3. **Phased Adoption:** Clients can choose when to upgrade to a new version, providing flexibility
   and control over how and when changes are adopted.

### **Common Versioning Strategies**

Versioning can be implemented in different ways, each with its pros and cons. Here are some common
strategies:

1. **URL Versioning:** Includes the version number in the API's URL. It's transparent and simple to
   use but can lead to URL changes over time.
    - Example: `/v1/users`, `/v2/users`
2. **Header Versioning:** Utilizes HTTP headers to specify the version. It keeps the URL clean but
   can be less discoverable.
    - Example: `Accept: application/vnd.myapi.v1+json`
3. **Media Type Versioning:** Defines the version through the media type in the content negotiation
   process.
    - Example: `application/vnd.myapi+json; version=1.0`
4. **Parameter Versioning:** Allows specifying the version as a request parameter. It's flexible but
   might be considered less elegant.
    - Example: `/users?version=1`

### **Considerations for Effective Versioning**

When implementing versioning, consider the following to ensure a smooth transition between versions:

1. **Clear Documentation:** Clearly document the differences between versions, including any
   deprecations or breaking changes.
2. **Communication with Consumers:** Inform users of your API about new versions, timelines for
   deprecations, and provide support for upgrading.
3. **Avoid Unnecessary Versions:** Only create new versions when essential, as having too many
   versions can lead to maintenance challenges.
4. **Provide Migration Tools or Guides:** If possible, offer tools or guides to assist clients in
   migrating from one version to another.

### **Conclusion**

Versioning is an essential aspect of API design, ensuring that APIs remain coherent, clean, and
easily adaptable to future changes. By considering the various strategies and associated best
practices, API providers can create an environment where both old and new clients can coexist and
thrive.

## Conclusion

For small projects, REST APIs are most commonly used for dynamic page updates. They should
efficiently handle user interactions, ideally mapping one user action to a single API request.
Moreover, REST APIs should be layered over faster, direct programming APIs to ensure swift access
when needed. Always weigh the benefits against the costs before deciding to implement REST APIs.
