# Boolean Arguments

When you use Boolean arguments in function calls, the code can become unclear and hard to
understand. For example:

```php
save($file, true, false, false, true);
```

In this call, it's not immediately obvious what each `true` or `false` represents. You would need to
look at the function definition to understand what each Boolean value is supposed to control. This
can lead to confusion and errors, especially if the function has many Boolean parameters.

## Named Integer Flags

Instead of using Boolean arguments, you can use named integer flags. This approach makes the
function calls more readable and self-explanatory. For example:

```php
define('OVERWRITE', 1);
define('DEFER', 2);

save($file, OVERWRITE | DEFER);
```

In this case, `OVERWRITE` and `DEFER` are constants that represent specific options. The bitwise OR
operator (`|`) is used to combine these options. This way, the function call is much clearer, and
you can easily understand what options are being passed to the function without needing to look at
the function definition.

## Benefits

-   **Readability**: The function call is more descriptive and easier to understand.
-   **Maintainability**: It's easier to add or remove options without changing the function
    signature.
-   **Error Reduction**: Reduces the likelihood of passing arguments in the wrong order or using
    incorrect values.

## Example Implementation

Here's an example of how you might implement this in PHP:

```php
define('OVERWRITE', 1);
define('DEFER', 2);
define('BACKUP', 4);

function save($file, $flags) {
    if ($flags & OVERWRITE) {
        // Handle overwrite
    }
    if ($flags & DEFER) {
        // Handle defer
    }
    if ($flags & BACKUP) {
        // Handle backup
    }
}

// Usage
save($file, OVERWRITE | DEFER);
```

In this example, the `save` function checks which flags are set using the bitwise AND operator
(`&`). This makes the function call more intuitive and the code easier to maintain.

DSG 2024-06-16
