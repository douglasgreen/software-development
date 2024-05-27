# Defining Exceptions

Each library should define a base exception with the library name:
`LibraryNameException`. This exception should not be thrown directly.

Instead, create a standard hierarchy of exceptions and extend from it instead.
Exceptions should be named like ObjectConditionException, where the Object is
experiencing the error condition.

Here is the standard hierarchy:

FileException - base class for file-related errors
FileNotFoundException extends FileException -  file doesn't exist
FileOpeningException extends FileException -  can't open a file
FileReadingException extends FileException -  file is not readable
FileWritingException extends FileException -  file is not writable

LogicException - base class for logic-related errors
OperationOrderException extends LogicException - did operations in wrong order
ParseException extends LogicException - unable to parse a string
RegexException extends LogicException - regex returned false when applied

DataException - base class for data-related errors
InputInvalidException extends DataException - passed a bad argument
IdDuplicateException extends DataException - ID duplicate when it should be unique

## Loading

Put all your exception definitions into one file called `Exceptions.php` and
load them using `composer.json` like this:

```
{
    "autoload": {
        "psr-4": {
            "YourNamespace\\": "src/"
        },
        "files": [
            "src/Exceptions.php"
        ]
    }
}
```
