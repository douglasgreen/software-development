# Code and Documentation Standards Guide

## Introduction

Coding standards are vital conventions that define how code is written and
structured. They play an essential role in maintaining consistency, boosting
collaboration, and ensuring the reliability of our software. This guide will
delve into the significance of these standards and our specific practices in the
PageMaker framework.

## Why adopt coding standards?

### Benefits

1. **Consistency Across Projects:** By having a clear set of standards, the code
   remains consistent across various projects, facilitating code reuse.
2. **Collaboration:** A unified coding style ensures that multiple programmers
   can work together more effectively.
3. **Clarity:** Well-structured code helps developers understand the overall
   architecture and components without unnecessary variation.
4. **Efficiency:** By setting conventions, developers can avoid unnecessary
   debates and confusion about code organization and presentation.

### Categories

1. **Architectural Standards:** Define higher-level guidelines about the
   structure of the software, such as layering and modularity.
2. **Naming Conventions:** Provide a standardized vocabulary for identifiers.
3. **Formatting Standards:** Dictate the layout of the code, including
   indentation, white space usage, and punctuation placement. For PHP, the PSR
   formatting standards apply, and their adherence is ensured using automated
   tools.

Automated tools are recommended for enforcing standards, especially lower-level
ones. This reduces the need to remember numerous rules and ensures consistent
application.

## When should I define standards?

1. **Collaboration:** To ensure the joint efforts of developers align
   seamlessly.
2. **Understanding:** To ensure clarity about how various components work
   together.
3. **Efficiency:** To make proactive decisions that save time later by
   eliminating debates on trivial issues.

## When should I not define standards?

1. **Limiting Essential Variation:** Avoid standards that disregard essential
   variances.
2. **Over-restriction:** Don't ban techniques based on a single misuse. For
   instance, prohibiting `if` or `switch` statements due to one poor
   implementation is impractical.
3. **Over-complication:** If standards are too minor and plentiful, they become
   cumbersome and counterproductive.
4. **Ambiguity:** Avoid standards that can be interpreted in multiple ways,
   causing confusion about compliance.

## PageMaker project standards

### Organizational standards

These standards are detailed in other documents.

### Formatting

1. **URL Components:** Use underscores and lowercase for all public-facing URL
   components, including code and executable files.
2. **Identifiers:** Adopt camel case for code and file identifiers, unless
   conflicting with PSR or other established conventions.
3. **Namespaces & Class Names:** Start with an uppercase letter.

### Naming

1. **Database Tables:** Use plural or category names.
2. **Namespaces:** Use the singular category name.
3. **File Directories:** Adopt the singular form.
4. **Public Names:** Prefer full words over abbreviations for all public-facing,
   non-local names.

### Documentation

1. **Focus:** Each document should target a single topic and audience.
2. **Style:** Frame documentation as a series of user-focused questions and
   direct answers. This approach emphasizes user needs and intentions.
3. **Completion:** Once a document is deemed complete, mark it with a signature,
   date, and a note if ChatGPT assisted in its creation.

Adhering to these standards will ensure that our code remains consistent, easy
to understand, and adaptable for future modifications.

<!-- DSG/ChatGPT 7/25/2023 -->
