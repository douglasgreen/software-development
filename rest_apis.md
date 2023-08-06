# Understanding REST APIs: A Guide

## Introduction

REST APIs provide a structured way to interact with web resources. Before diving into the details, let's clarify when and why one might use them, especially in the context of smaller projects or in-page animations.

## When to use REST APIs

REST APIs are ideal when:

1. **Partial Page Updates**: You need to update only a part of your web page without reloading the entire page. This is particularly relevant for in-page animations or dynamic content updates.
2. **Scalability**: Your project might grow and need to scale beyond a single server.
3. **Multi-language Support**: Your application might be consumed by clients written in various programming languages. REST APIs offer a universal interaction protocol.
4. **External Access**: You intend to allow third parties to interact with your application.

## Structuring REST APIs

### Endpoints organization

Endpoints, or the specific URLs of your API where resources can be accessed, can reside within your main project. This means you don't necessarily need to spin off a separate project for your API. This integrated approach lets you reuse the existing database connection and the HTTP host.

### Scalability aspects

The term 'scalable' in the context of REST APIs can be viewed in two dimensions:

1. **Throughput**: APIs can manage increased loads when dedicated servers handle them.
2. **Latency**: Each API call requires network data transfer, which introduces some delay. This latency becomes more prominent when you break down your application into multiple microservices.

## REST APIs: modularity and costs

Let's understand REST API modularity using PHP as our base:

1. **Direct PHP API**: This is the most straightforward approach where your code is broken down into classes, and they're loaded as needed. It's efficient and offers the advantage of direct, fast function calls.
2. **Project-based Modularity with Composer**: Similar to the direct approach but the code is separated into a different repository. It provides better separation but requires managing multiple repositories.
3. **Microservice Approach with REST API**: Here, your project is transformed into an independent microservice accessible via a REST API. 

**Benefits**:
- **Isolation**: Your code remains encapsulated, promoting better clarity.
- **Flexibility**: The code can be executed on a different server or can support multiple programming languages.

**Costs**:
- **Data Fragmentation**: The data might be split across multiple sources, complicating relationships like foreign keys.
- **Setup Overhead**: Additional setup and authentication layers are introduced.
- **Performance Overheads**: Network data transfer introduces latency, and direct PHP access is usually faster than API calls.

### Key considerations

1. **Versioning**: Whether you use direct PHP, Composer, or REST APIs, you always have the flexibility to version your application.
2. **Modularity**: REST APIs inherently promote modularity, but remember, modular design can be achieved even without network isolation.

## Conclusion

For small projects, REST APIs are most commonly used for dynamic page updates. They should efficiently handle user interactions, ideally mapping one user action to a single API request. Moreover, REST APIs should be layered over faster, direct programming APIs to ensure swift access when needed. Always weigh the benefits against the costs before deciding to implement REST APIs.
