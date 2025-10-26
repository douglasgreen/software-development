## CORE PRINCIPLES

When generating PHP code, always follow these principles:

1. **PSR Compliance**: Follow PSR-12 (coding style), PSR-4 (autoloading), and PSR-7/15 (HTTP)
2. **SOLID Principles**: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Injection
3. **Security First**: Validate input, escape output, use prepared statements, avoid eval()
4. **Type Safety**: Use strict types, type hints, and return type declarations
5. **Modern PHP**: Target PHP 8.1+ features (enums, readonly properties, named arguments, etc.)

---

## CODE STYLE

```php
<?php

declare(strict_types=1);

namespace App\Domain\User;

use App\Domain\Email\EmailAddress;
use DateTimeImmutable;

/**
 * Represents a user in the system.
 */
final class User
{
    public function __construct(
        private readonly string $id,
        private string $name,
        private EmailAddress $email,
        private readonly DateTimeImmutable $createdAt,
    ) {
        $this->validateName($name);
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function changeName(string $name): void
    {
        $this->validateName($name);
        $this->name = $name;
    }

    private function validateName(string $name): void
    {
        if (trim($name) === '') {
            throw new \InvalidArgumentException('Name cannot be empty');
        }
    }
}
```

**Rules:**
- Always use `declare(strict_types=1)` at the top
- 4 spaces for indentation (never tabs)
- Opening braces on same line for methods/functions
- Use `final` by default for classes (inheritance should be intentional)
- Constructor property promotion for PHP 8.0+
- One blank line between methods

---

## NAMING CONVENTIONS

```php
// Classes: PascalCase
class UserRepository {}
class PaymentProcessor {}

// Methods/Functions: camelCase
public function calculateTotal(): float {}
private function validateInput(): void {}

// Variables: camelCase
$userName = 'John';
$isActive = true;

// Constants: UPPER_SNAKE_CASE
private const MAX_LOGIN_ATTEMPTS = 3;
public const DEFAULT_TIMEOUT = 30;

// Interfaces: PascalCase with descriptive names
interface UserRepositoryInterface {}
interface PaymentGateway {}

// Traits: PascalCase with adjective or capability
trait Timestampable {}
trait Loggable {}

// Enums: PascalCase for enum, UPPER_SNAKE_CASE for cases
enum OrderStatus: string
{
    case PENDING = 'pending';
    case COMPLETED = 'completed';
    case CANCELLED = 'cancelled';
}
```

---

## DEPENDENCY INJECTION

Always use constructor injection, never service locators or global state:

```php
<?php

declare(strict_types=1);

namespace App\Application\User;

use App\Domain\User\UserRepositoryInterface;
use App\Domain\Email\EmailServiceInterface;
use Psr\Log\LoggerInterface;

final class CreateUserHandler
{
    public function __construct(
        private readonly UserRepositoryInterface $userRepository,
        private readonly EmailServiceInterface $emailService,
        private readonly LoggerInterface $logger,
    ) {}

    public function handle(CreateUserCommand $command): void
    {
        $user = new User(
            id: $command->id,
            email: $command->email,
            name: $command->name,
        );

        $this->userRepository->save($user);

        try {
            $this->emailService->sendWelcomeEmail($user);
        } catch (\Exception $e) {
            $this->logger->error('Failed to send welcome email', [
                'user_id' => $user->getId(),
                'error' => $e->getMessage(),
            ]);
        }
    }
}
```

---

## DATABASE INTERACTIONS

Always use prepared statements and repository pattern:

```php
<?php

declare(strict_types=1);

namespace App\Infrastructure\User;

use App\Domain\User\User;
use App\Domain\User\UserRepositoryInterface;
use PDO;

final class PdoUserRepository implements UserRepositoryInterface
{
    public function __construct(
        private readonly PDO $connection
    ) {}

    public function findById(string $id): ?User
    {
        $stmt = $this->connection->prepare(
            'SELECT * FROM users WHERE id = :id LIMIT 1'
        );
        $stmt->execute(['id' => $id]);

        $row = $stmt->fetch(PDO::FETCH_ASSOC);

        if ($row === false) {
            return null;
        }

        return $this->hydrateUser($row);
    }

    public function save(User $user): void
    {
        $stmt = $this->connection->prepare(
            'INSERT INTO users (id, name, email, created_at)
             VALUES (:id, :name, :email, :created_at)
             ON DUPLICATE KEY UPDATE name = :name, email = :email'
        );

        $stmt->execute([
            'id' => $user->getId(),
            'name' => $user->getName(),
            'email' => $user->getEmail()->toString(),
            'created_at' => $user->getCreatedAt()->format('Y-m-d H:i:s'),
        ]);
    }

    private function hydrateUser(array $row): User
    {
        return new User(
            id: $row['id'],
            name: $row['name'],
            email: new EmailAddress($row['email']),
            createdAt: new \DateTimeImmutable($row['created_at']),
        );
    }
}
```

---

## LAYERED ARCHITECTURE

Structure code in clear layers:

```
src/
├── Domain/              # Business logic, entities, value objects
│   ├── User/
│   │   ├── User.php
│   │   ├── UserRepositoryInterface.php
│   │   └── UserNotFoundException.php
│   └── Email/
│       └── EmailAddress.php
├── Application/         # Use cases, commands, handlers
│   └── User/
│       ├── CreateUserCommand.php
│       └── CreateUserHandler.php
├── Infrastructure/      # External concerns (DB, APIs, files)
│   ├── User/
│   │   └── PdoUserRepository.php
│   └── Email/
│       └── SmtpEmailService.php
└── Presentation/        # Controllers, CLI commands
    └── Http/
        └── UserController.php
```

**Example Controller:**

```php
<?php

declare(strict_types=1);

namespace App\Presentation\Http;

use App\Application\User\CreateUserCommand;
use App\Application\User\CreateUserHandler;
use Psr\Http\Message\ResponseInterface;
use Psr\Http\Message\ServerRequestInterface;

final class UserController
{
    public function __construct(
        private readonly CreateUserHandler $createUserHandler,
    ) {}

    public function create(ServerRequestInterface $request): ResponseInterface
    {
        $data = json_decode($request->getBody()->getContents(), true);

        // Validate input
        $errors = $this->validateCreateUserData($data);
        if (!empty($errors)) {
            return $this->jsonResponse(['errors' => $errors], 400);
        }

        // Execute use case
        $command = new CreateUserCommand(
            id: $this->generateId(),
            name: $data['name'],
            email: $data['email'],
        );

        $this->createUserHandler->handle($command);

        return $this->jsonResponse(['success' => true], 201);
    }

    private function validateCreateUserData(?array $data): array
    {
        $errors = [];

        if (!isset($data['name']) || trim($data['name']) === '') {
            $errors['name'] = 'Name is required';
        }

        if (!isset($data['email']) || !filter_var($data['email'], FILTER_VALIDATE_EMAIL)) {
            $errors['email'] = 'Valid email is required';
        }

        return $errors;
    }

    private function jsonResponse(array $data, int $status): ResponseInterface
    {
        // Implementation depends on PSR-7 factory
    }

    private function generateId(): string
    {
        return bin2hex(random_bytes(16));
    }
}
```

---

## VALUE OBJECTS

Encapsulate primitive types with validation:

```php
<?php

declare(strict_types=1);

namespace App\Domain\Email;

final class EmailAddress
{
    private readonly string $value;

    public function __construct(string $email)
    {
        $normalized = strtolower(trim($email));

        if (!filter_var($normalized, FILTER_VALIDATE_EMAIL)) {
            throw new \InvalidArgumentException(
                "Invalid email address: {$email}"
            );
        }

        $this->value = $normalized;
    }

    public function toString(): string
    {
        return $this->value;
    }

    public function equals(EmailAddress $other): bool
    {
        return $this->value === $other->value;
    }
}
```

---

## ERROR HANDLING

Use exceptions for exceptional cases, not control flow:

```php
<?php

declare(strict_types=1);

namespace App\Domain\User;

// Domain-specific exceptions
final class UserNotFoundException extends \RuntimeException
{
    public static function withId(string $id): self
    {
        return new self("User with ID {$id} not found");
    }
}

final class InvalidUserDataException extends \InvalidArgumentException
{
    public static function emptyName(): self
    {
        return new self('User name cannot be empty');
    }
}

// Usage
public function updateUser(string $id, string $name): void
{
    $user = $this->userRepository->findById($id);

    if ($user === null) {
        throw UserNotFoundException::withId($id);
    }

    try {
        $user->changeName($name);
    } catch (InvalidUserDataException $e) {
        // Handle validation error
        $this->logger->warning('Invalid user data', [
            'user_id' => $id,
            'error' => $e->getMessage(),
        ]);
        throw $e;
    }

    $this->userRepository->save($user);
}
```

---

## SECURITY CHECKLIST

Always apply these security practices:

```php
<?php

// ✅ Input Validation
$email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
if ($email === false) {
    throw new \InvalidArgumentException('Invalid email');
}

// ✅ Prepared Statements (NEVER string concatenation)
$stmt = $pdo->prepare('SELECT * FROM users WHERE email = :email');
$stmt->execute(['email' => $email]);

// ✅ Output Escaping
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');

// ✅ Password Hashing
$hash = password_hash($password, PASSWORD_ARGON2ID);
$isValid = password_verify($inputPassword, $hash);

// ✅ CSRF Protection
if (!hash_equals($_SESSION['csrf_token'], $_POST['csrf_token'])) {
    throw new SecurityException('Invalid CSRF token');
}

// ✅ File Upload Validation
$allowedMimeTypes = ['image/jpeg', 'image/png'];
$finfo = finfo_open(FILEINFO_MIME_TYPE);
$mimeType = finfo_file($finfo, $_FILES['upload']['tmp_name']);

if (!in_array($mimeType, $allowedMimeTypes, true)) {
    throw new \RuntimeException('Invalid file type');
}

// ❌ NEVER use eval(), exec() with user input, or disable security features
```

---

## TESTING STRUCTURE

Write testable code with clear interfaces:

```php
<?php

declare(strict_types=1);

namespace Tests\Application\User;

use App\Application\User\CreateUserHandler;
use App\Domain\User\UserRepositoryInterface;
use PHPUnit\Framework\TestCase;

final class CreateUserHandlerTest extends TestCase
{
    public function testCreatesUserSuccessfully(): void
    {
        // Arrange
        $userRepository = $this->createMock(UserRepositoryInterface::class);
        $userRepository->expects($this->once())
            ->method('save')
            ->with($this->callback(function ($user) {
                return $user->getName() === 'John Doe';
            }));

        $handler = new CreateUserHandler($userRepository);
        $command = new CreateUserCommand(
            id: '123',
            name: 'John Doe',
            email: 'john@example.com',
        );

        // Act
        $handler->handle($command);

        // Assert is implicit in the mock expectation
    }
}
```

---

## ADDITIONAL RULES

1. **Avoid static methods** except for factories or pure functions
2. **Use immutability** where possible (readonly properties, DateTimeImmutable)
3. **Null should be exceptional** - prefer explicit types or Option types
4. **No mixed types** - always specify concrete types
5. **Avoid arrays for structured data** - use DTOs/Value Objects
6. **Composition over inheritance** - prefer interfaces and composition
7. **Single exit point** is not required - use early returns for guard clauses
8. **No magic numbers** - use named constants
9. **Comments explain why, not what** - code should be self-documenting
10. **Keep functions small** - aim for < 20 lines per method
11. **Descriptive names** - don't use single-letter variable names.

---

## QUICK REFERENCE TEMPLATE

When generating PHP code, use this template:

```php
<?php

declare(strict_types=1);

namespace [Appropriate\Namespace];

// Imports grouped and alphabetized
use App\Domain\...;
use Psr\...;

/**
 * [Class description - what it does, not how]
 */
final class [ClassName]
{
    public function __construct(
        private readonly [Type] $dependency,
    ) {}

    public function [methodName]([Type] $param): [ReturnType]
    {
        // Guard clauses first
        if ([invalid condition]) {
            throw new \InvalidArgumentException('[Clear message]');
        }

        // Main logic
        $result = $this->dependency->doSomething($param);

        return $result;
    }
}
