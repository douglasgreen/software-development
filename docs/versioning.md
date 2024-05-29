# Comprehensive Versioning

## Overview

In the PageMaker system of internal versioning, every piece of code and content,
whether public or private, is subjected to versioning. This ensures
traceability, manageability, and backward compatibility.

-   **Initial Version**: The project starts with a 'dev' version, indicating a
    development or pre-release stage.
-   **Major Releases**: As the project matures, major releases are versioned as
    v1, v2, and so on.
-   **Directory-based Versioning**: Each version of the content is placed in a
    separate directory named after that version. This provides a clear
    separation and organization of content based on versions.
-   **Autoload Versioning**: The versioning extends to the autoload
    configuration. The version name is used in the path to determine which
    version of the code should be loaded. For instance, the `PageMakerDev\\`
    namespace points to the `dev/app/` directory, while `PageMakerV1\\` points
    to the `v1/app/`.
-   **Composer Versioning**: The major version in the composer is set to the
    highest major release version available.
-   **Dependency Management**: Any component that relies on a particular major
    release version must be updated to that version. This ensures compatibility
    and reduces the risk of breaking changes.

## Comparison to REST API versioning

REST API versioning is a strategy used to manage changes in APIs over time
without breaking the applications that depend on them.

-   **URI Versioning**: The most common method where the version number is
    included in the URI, e.g., `/v1/users`.
-   **Header Versioning**: The version information is sent in the request
    header.
-   **Parameter Versioning**: The version is passed as a parameter in the
    request.
-   **Media Type Versioning**: The version is included in the accept header,
    specifying a custom media type.

## Pros and cons

**Pros of Internal Content Versioning**

1. **Clear Organization**: By segregating content based on versions, it's easier
   to locate and manage specific versions of the content.
2. **Backward Compatibility**: Older versions of the content remain accessible,
   ensuring that any system depending on an older version isn't broken.
3. **Flexibility**: Components can be upgraded individually, allowing for
   gradual updates.

**Cons of Internal Content Versioning**

1. **Complexity**: Managing multiple versions can become complex, especially
   when there are dependencies between components.
2. **Storage Overhead**: Storing multiple versions can lead to increased storage
   requirements.

**Pros of REST API Versioning**

1. **Consistency**: Clients know what to expect from the API, regardless of the
   changes in the backend.
2. **Flexibility**: Allows developers to introduce non-breaking changes without
   affecting existing clients.

**Cons of REST API Versioning**

1. **Maintenance Overhead**: Maintaining multiple versions of an API can be
   challenging.
2. **Potential Confusion**: If not documented well, clients might get confused
   about which version to use.

## Uniform versioning approach

It's essential to maintain consistency in versioning semantics throughout all
components of a project. This standard approach ensures clarity and coherence:

-   **Databases**: For instance, a "Sample" database can adopt versions like
    `SampleDev`, `SampleV1`, and so forth.
-   **Assets**: Directories containing assets, such as `images`, should follow a
    naming convention like `images_dev`, `images_v1`, etc.
-   **Web Document Root**: The root can be organized into specific
    subdirectories based on versions, e.g., `dev`, `v1`, and so on.

The key takeaway is adopting a unified, incremental versioning strategy across
the project, ensuring structured and consistent version labeling.

## Handling versioning with Composer and PageMaker

### Composer Limitations:

Composer has an inherent constraint: it can't accommodate multiple versions of a
library simultaneously, posing challenges during upgrades.

### PageMaker's Solution:

In contrast, PageMaker offers an integrated library versioning mechanism. It
permits the coexistence of a development version and multiple release versions
of its library in the same project. This versatility facilitates developers in
upgrading distinct project segments individually.

For Composer:

-   Using the `PageMaker` namespace signifies the latest version.
-   For specific versions, aliases like `PageMakerV1` should be adopted.

However, a significant limitation arises with Composer dependencies since they
don't support multiple versioning.

## Conclusion

Versioning, whether for a PHP project's internal content or a REST API, plays a
pivotal role in tracking and managing evolutionary changes. While internal
content versioning focuses on orderly code and content arrangement within a
project, REST API versioning ensures consistent external application
interactions with the service. Opting for one or integrating both hinges on the
project's unique requirements and its external system engagements.

<!-- DSG/ChatGPT 7/26/2023 -->
