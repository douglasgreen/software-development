# Web-Last Architecture

In contemporary software design, web-centric architectures dominate. However, I propose a paradigm shift: prioritize the command-line over the web interface. By doing so, you ensure that the core functionality of your program operates independently of network transmission.

## Design philosophy

1. **Command-Line Centricity**: Begin with a comprehensive command-line application. This application should encapsulate all the primary functionalities of your program. Such an approach facilitates
    - Scripting capabilities by stringing together command sequences.
    - Comprehensive automated testing.
2. **Web Layer as an Add-On**: Once your command-line base is solid, introduce the web layer. This ensures that the core logic remains unaffected by the constraints and peculiarities of web design and operations.

## Rationale

### Limitations of web-centric design

- **Simplicity and Time-outs**: Web architectures are tailored for straightforward commands and are prone to time-outs.
- **Data Input Constraints**: HTML forms have restrictions on the volume of input data.
- **PHP Session Issues**: PHP sessions can complicate matters by serializing data and inadvertently creating persistent state.
- **JavaScript Challenges**: 
  - Transforming your application into a single-page app often introduces unnecessary long-term state maintenance.
  - It superimposes functionality on pre-rendered HTML layers.
- **CSS Concerns**: CSS lacks modularity, which hinders advanced styling and sharing third-party styles.
- **REST API Pitfalls**: These can segment data and cause undue data transport across networks, leading to latency and unpredictability.
- **Complexity and Bloat**: The comprehensive web stack frequently introduces extraneous dependencies, resulting in unwarranted complexity, bloat, and frequent updates.

### Merits of command-line first design

- **No Time-out Issues**: Allows processing of substantial data volumes without timing out.
- **Unbounded Data Inputs**: Accepts data without inherent limitations.
- **Session Independence**: Avoids persistent state across requests.
- **Architectural Simplicity**: Omits single-page app structure and doesn't try to manipulate a pre-rendered document layer.
- **Emphasis on Data Processing**: Prioritizes data operations over stylistic rendering.
- **Network Efficiency**: Sidesteps unnecessary network layers.
- **Minimized Dependencies**: Bypasses the bulk of web dependencies, keeping the architecture lean.

In summary, focus initially on building a robust command-line model and controllers. The web layer should be an afterthought, ensuring the primary functions are not compromised by web-based challenges.

<!-- DSG/ChatGPT 8/4/2023 -->
