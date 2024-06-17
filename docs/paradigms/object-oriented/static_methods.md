# Static Methods and Classes

When using static classes and functions in PHP, it's important to follow best practices to ensure
maintainability, readability, and proper functionality. Here are some key guidelines:

### 1. **Use Static Methods for Utility Functions**

Static methods are ideal for utility functions that do not require object state. These methods can
be called without creating an instance of the class.

```php
class MathUtils {
    public static function add($a, $b) {
        return $a + $b;
    }
}

// Usage
$result = MathUtils::add(5, 10);
```

### 2. **Avoid Using Static Methods for Stateful Operations**

Static methods should not be used for operations that depend on or modify the state of an object.
This can lead to code that is difficult to test and maintain.

### 3. **Singleton Pattern**

For classes that should only have one instance, use the Singleton pattern. This ensures that a class
has only one instance and provides a global point of access to it.

```php
class Singleton {
    private static $instance = null;
    private $name;

    private function __construct() {
        $this->name = 'SingletonInstance';
    }

    public static function getInstance() {
        if (self::$instance == null) {
            self::$instance = new Singleton();
        }
        return self::$instance;
    }

    public function getName() {
        return $this->name;
    }
}

// Usage
$instance = Singleton::getInstance();
echo $instance->getName();
```

### 4. **Late Static Bindings**

Use `static::` instead of `self::` when you want to ensure that the method call is bound to the
class where it is called, not where it is defined. This is useful in inheritance scenarios.

```php
class Base {
    public static function who() {
        echo __CLASS__;
    }

    public static function test() {
        static::who(); // Late static binding
    }
}

class Child extends Base {
    public static function who() {
        echo __CLASS__;
    }
}

Child::test(); // Outputs "Child"
```

### 5. **Static Properties**

Static properties are shared across all instances of a class. Use them when you need a property that
is common to all instances. But realize when you use them that they are a form of global state that
makes testing more difficult.

```php
class Counter {
    public static $count = 0;

    public function __construct() {
        self::$count++;
    }
}

// Usage
new Counter();
new Counter();
echo Counter::$count; // Outputs 2
```

### 6. **Make Methods Without $this Static**

If a class has methods that make no reference to the current object `$this`, then you should make
them static. That tells the caller that the method is not interacting with the object properties.

### 7. **Static Initialization**

PHP does not support static constructors directly. You can simulate this by calling a static
initialization method after the class definition.

```php
class MyClass {
    public static $initialized = false;

    public static function init() {
        if (!self::$initialized) {
            // Initialization code
            self::$initialized = true;
        }
    }
}

MyClass::init();
```

### 8. **Accessing Static Members**

Access static properties and methods using the class name and the scope resolution operator `::`.

```php
class Example {
    public static $staticVar = 'static value';

    public static function staticMethod() {
        return 'static method';
    }
}

// Usage
echo Example::$staticVar; // Outputs 'static value'
echo Example::staticMethod(); // Outputs 'static method'
```

### 9. **Avoid Static Methods for Dependency Injection**

Static methods make it difficult to use dependency injection, which can lead to tightly coupled
code. Prefer instance methods for better testability and flexibility.

### 10. **Documentation and Comments**

Document the purpose and usage of static methods and properties clearly. This helps other developers
understand the intent and proper usage of your code.

By following these best practices, you can effectively use static classes and functions in PHP while
maintaining clean, maintainable, and testable code.

DSG 2024-06-17
