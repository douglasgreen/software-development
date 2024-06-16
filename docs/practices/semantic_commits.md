# Semantic Commits

Here are the descriptions for each of the semantic commit types. They are written in the order that
you should prefer them.

## Changes to non-application areas

-   **build**: Changes that affect the build system or external dependencies. Examples include
    updates to build tools like gulp, broccoli, or npm or updates to package versions.

-   **test**: Adding missing tests or correcting existing tests. This type of commit is used for
    changes related to testing the codebase.

-   **ci**: Changes to Continuous Integration (CI) configuration files and scripts. Examples include
    updates to Travis, CircleCI, BrowserStack, or SauceLabs configurations.

## Changes that affect functionality

-   **feat**: A new feature for the user. This type of commit introduces new functionality to the
    codebase.

-   **fix**: A bug fix. This type of commit addresses a bug in the codebase.

-   **perf**: A code change that improves performance. This type of commit optimizes the code to
    make it run faster or more efficiently.

## Changes that don't affect functionality

-   **refactor**: A code change that neither fixes a bug nor adds a feature. This includes code
    restructuring, renaming variables, deleting unused code, or other improvements to the code’s
    structure without changing its behavior.

-   **style**: Changes that do not affect the meaning of the code. This includes formatting changes,
    adding or removing white-space, and other non-functional changes.

-   **chore**: Routine tasks that do not affect the application’s functionality. Examples include
    updating grunt tasks, modifying `.gitignore`, or other maintenance tasks.

-   **revert**: Reverts a previous commit. This type of commit undoes changes made by a previous
    commit.

## Changes to documentation

-   **docs**: Documentation-only changes. This includes updates to README files, inline
    documentation, or other project documentation.
