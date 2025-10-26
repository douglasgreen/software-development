# JavaScript Coding Standards for LLM Code Generation

## Core Principles

When generating JavaScript code, always follow these principles:

1. **Clarity over cleverness** - Write explicit, readable code
2. **Functional composition** - Prefer pure functions and immutability
3. **Error handling first** - Always handle errors explicitly
4. **Modern ES6+** - Use current JavaScript features
5. **Single responsibility** - Each function/module does one thing well
6. **DRY with pragmatism** - Avoid duplication, but don't over-abstract

## Code Style Standards

### Naming Conventions
- **Variables/Functions**: `camelCase`
- **Constants**: `UPPER_SNAKE_CASE` for true constants, `camelCase` for config objects
- **Classes/Components**: `PascalCase`
- **Private fields**: `#privateField` or `_privateField` prefix
- **Boolean variables**: Use `is`, `has`, `should` prefixes (e.g., `isActive`, `hasPermission`)

```javascript
// Good
const MAX_RETRY_ATTEMPTS = 3;
const userConfig = { timeout: 5000 };
class UserService {}
function calculateTotal() {}
const isValid = true;

// Avoid
const max_retry = 3;
const UserConfig = {};
function calc() {}
const valid = true;
```

### Function Design

```javascript
// ✅ GOOD: Pure function, single responsibility, clear name
function calculateOrderTotal(items, taxRate) {
  if (!Array.isArray(items) || typeof taxRate !== 'number') {
    throw new TypeError('Invalid arguments');
  }

  const subtotal = items.reduce((sum, item) => sum + item.price, 0);
  return subtotal * (1 + taxRate);
}

// ❌ AVOID: Side effects, multiple responsibilities, unclear
let total = 0;
function process(items) {
  total = items.reduce((s, i) => s + i.price, 0);
  total = total * 1.1;
  console.log(total);
  return total;
}
```

### Arrow Functions vs Regular Functions

```javascript
// Use arrow functions for: callbacks, array methods, short functions
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(n => n * 2);
const asyncFetch = async (url) => await fetch(url);

// Use regular functions for: methods, functions needing 'this' context, constructors
class DataService {
  constructor(apiUrl) {
    this.apiUrl = apiUrl;
  }

  async fetchData(endpoint) {
    return await fetch(`${this.apiUrl}/${endpoint}`);
  }
}
```

## Error Handling

### Always Handle Errors Explicitly

```javascript
// ✅ GOOD: Explicit error handling
async function fetchUserData(userId) {
  try {
    if (!userId) {
      throw new Error('userId is required');
    }

    const response = await fetch(`/api/users/${userId}`);

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }

    return await response.json();
  } catch (error) {
    console.error('Failed to fetch user data:', error);
    throw new Error(`User fetch failed: ${error.message}`);
  }
}

// ❌ AVOID: Silent failures or bare try-catch
async function fetchUserData(userId) {
  try {
    const response = await fetch(`/api/users/${userId}`);
    return await response.json();
  } catch (error) {
    console.log(error); // Don't just log and continue
  }
}
```

### Custom Error Classes

```javascript
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = 'ValidationError';
    this.field = field;
  }
}

class NotFoundError extends Error {
  constructor(resource, id) {
    super(`${resource} with id ${id} not found`);
    this.name = 'NotFoundError';
    this.statusCode = 404;
  }
}

// Usage
function validateEmail(email) {
  if (!email.includes('@')) {
    throw new ValidationError('Invalid email format', 'email');
  }
  return true;
}
```

## Async/Await Patterns

```javascript
// ✅ GOOD: Parallel execution when possible
async function fetchDashboardData(userId) {
  try {
    const [user, posts, comments] = await Promise.all([
      fetchUser(userId),
      fetchUserPosts(userId),
      fetchUserComments(userId)
    ]);

    return { user, posts, comments };
  } catch (error) {
    throw new Error(`Dashboard data fetch failed: ${error.message}`);
  }
}

// ❌ AVOID: Sequential when not necessary
async function fetchDashboardData(userId) {
  const user = await fetchUser(userId);
  const posts = await fetchUserPosts(userId); // Waits unnecessarily
  const comments = await fetchUserComments(userId); // Waits unnecessarily
  return { user, posts, comments };
}

// ✅ GOOD: Sequential when there are dependencies
async function createUserProfile(userData) {
  const user = await createUser(userData);
  const profile = await createProfile(user.id); // Needs user.id
  await sendWelcomeEmail(user.email); // Needs user.email
  return { user, profile };
}
```

## Object and Array Manipulation

```javascript
// ✅ GOOD: Immutable operations
function addItem(cart, newItem) {
  return [...cart, newItem];
}

function updateUser(user, updates) {
  return { ...user, ...updates, updatedAt: Date.now() };
}

function removeItem(items, itemId) {
  return items.filter(item => item.id !== itemId);
}

// ❌ AVOID: Mutating original data
function addItem(cart, newItem) {
  cart.push(newItem); // Mutates original
  return cart;
}
```

### Destructuring and Default Values

```javascript
// ✅ GOOD: Clear destructuring with defaults
function createUser({
  name,
  email,
  role = 'user',
  isActive = true
} = {}) {
  return { name, email, role, isActive, createdAt: Date.now() };
}

// Array destructuring
const [first, second, ...rest] = [1, 2, 3, 4, 5];
const [error, data] = await fetchData().then(d => [null, d]).catch(e => [e, null]);
```

## Module Structure

```javascript
// ✅ GOOD: Clear exports, organized structure
// userService.js
const API_BASE_URL = '/api/v1';

async function fetchUser(userId) {
  const response = await fetch(`${API_BASE_URL}/users/${userId}`);
  if (!response.ok) throw new Error('Fetch failed');
  return response.json();
}

async function updateUser(userId, data) {
  const response = await fetch(`${API_BASE_URL}/users/${userId}`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data)
  });
  if (!response.ok) throw new Error('Update failed');
  return response.json();
}

export { fetchUser, updateUser };

// Or default export for single primary export
export default class UserService {
  constructor(apiUrl) {
    this.apiUrl = apiUrl;
  }
  // methods...
}
```

## Comments and Documentation

```javascript
/**
 * Calculates the total price including tax and discount
 * @param {number} basePrice - The base price before calculations
 * @param {number} taxRate - Tax rate as decimal (e.g., 0.1 for 10%)
 * @param {number} [discount=0] - Optional discount as decimal
 * @returns {number} Final price rounded to 2 decimal places
 * @throws {TypeError} If parameters are not numbers
 */
function calculateFinalPrice(basePrice, taxRate, discount = 0) {
  if (typeof basePrice !== 'number' || typeof taxRate !== 'number') {
    throw new TypeError('Price and tax rate must be numbers');
  }

  const priceAfterDiscount = basePrice * (1 - discount);
  const finalPrice = priceAfterDiscount * (1 + taxRate);
  return Math.round(finalPrice * 100) / 100;
}

// Use inline comments sparingly, only for complex logic
const threshold = 100; // Orders above this amount get free shipping
```

## Data Validation

```javascript
// ✅ GOOD: Input validation with clear messages
function validateUserInput(data) {
  const errors = [];

  if (!data.email || !data.email.includes('@')) {
    errors.push({ field: 'email', message: 'Valid email is required' });
  }

  if (!data.password || data.password.length < 8) {
    errors.push({ field: 'password', message: 'Password must be at least 8 characters' });
  }

  if (errors.length > 0) {
    throw new ValidationError('Validation failed', errors);
  }

  return true;
}

// Type checking helper
function assertType(value, type, paramName) {
  if (typeof value !== type) {
    throw new TypeError(`${paramName} must be a ${type}`);
  }
}
```

## State Management Patterns

```javascript
// ✅ GOOD: Reducer pattern for complex state
function cartReducer(state, action) {
  switch (action.type) {
    case 'ADD_ITEM':
      return {
        ...state,
        items: [...state.items, action.payload],
        total: state.total + action.payload.price
      };

    case 'REMOVE_ITEM':
      const removedItem = state.items.find(item => item.id === action.payload);
      return {
        ...state,
        items: state.items.filter(item => item.id !== action.payload),
        total: state.total - (removedItem?.price || 0)
      };

    case 'CLEAR_CART':
      return { items: [], total: 0 };

    default:
      return state;
  }
}

// Usage
let cart = { items: [], total: 0 };
cart = cartReducer(cart, { type: 'ADD_ITEM', payload: { id: 1, price: 29.99 } });
```

## Testing Approach

```javascript
// Always write testable code with clear inputs/outputs
// ✅ GOOD: Pure, testable function
function formatCurrency(amount, currency = 'USD') {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency
  }).format(amount);
}

// Example tests you'd write:
// formatCurrency(100) => "$100.00"
// formatCurrency(1234.56) => "$1,234.56"
// formatCurrency(100, 'EUR') => "€100.00"

// ❌ AVOID: Difficult to test
function displayPrice(itemId) {
  const item = document.getElementById(itemId);
  const price = parseFloat(item.dataset.price);
  item.textContent = '$' + price.toFixed(2);
}
```

## Configuration and Constants

```javascript
// ✅ GOOD: Centralized configuration
const CONFIG = {
  API_BASE_URL: process.env.API_URL || 'http://localhost:3000',
  API_TIMEOUT: 5000,
  MAX_RETRIES: 3,
  CACHE_TTL: 60000,
  FEATURES: {
    enableBetaFeatures: false,
    enableAnalytics: true
  }
};

Object.freeze(CONFIG); // Prevent modifications

export default CONFIG;
```

## Design Patterns

### Factory Pattern
```javascript
class UserFactory {
  static create(type, data) {
    const baseUser = {
      id: crypto.randomUUID(),
      createdAt: Date.now(),
      ...data
    };

    switch (type) {
      case 'admin':
        return { ...baseUser, role: 'admin', permissions: ['all'] };
      case 'moderator':
        return { ...baseUser, role: 'moderator', permissions: ['read', 'write'] };
      default:
        return { ...baseUser, role: 'user', permissions: ['read'] };
    }
  }
}
```

### Dependency Injection
```javascript
// ✅ GOOD: Dependencies injected, easy to test
class OrderService {
  constructor(paymentService, emailService, database) {
    this.paymentService = paymentService;
    this.emailService = emailService;
    this.database = database;
  }

  async createOrder(orderData) {
    const payment = await this.paymentService.process(orderData.payment);
    const order = await this.database.orders.create({ ...orderData, payment });
    await this.emailService.sendConfirmation(order);
    return order;
  }
}
```

### Builder Pattern
```javascript
class QueryBuilder {
  constructor() {
    this.query = { filters: [], sorts: [], limit: 100 };
  }

  where(field, operator, value) {
    this.query.filters.push({ field, operator, value });
    return this;
  }

  orderBy(field, direction = 'asc') {
    this.query.sorts.push({ field, direction });
    return this;
  }

  limit(count) {
    this.query.limit = count;
    return this;
  }

  build() {
    return this.query;
  }
}

// Usage
const query = new QueryBuilder()
  .where('status', '=', 'active')
  .where('price', '>', 100)
  .orderBy('createdAt', 'desc')
  .limit(50)
  .build();
```

## Performance Considerations

```javascript
// ✅ GOOD: Memoization for expensive calculations
function memoize(fn) {
  const cache = new Map();

  return function(...args) {
    const key = JSON.stringify(args);

    if (cache.has(key)) {
      return cache.get(key);
    }

    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

const expensiveCalculation = memoize((n) => {
  // Complex calculation
  return n * n;
});

// ✅ GOOD: Debouncing user input
function debounce(fn, delay) {
  let timeoutId;

  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => fn.apply(this, args), delay);
  };
}

const handleSearch = debounce((query) => {
  // API call
}, 300);
```

## Summary Checklist

When generating code, ensure:
- [ ] Functions are pure when possible
- [ ] Errors are handled explicitly
- [ ] Variable names are descriptive
- [ ] No magic numbers (use named constants)
- [ ] Async operations use async/await
- [ ] Data is treated as immutable
- [ ] Dependencies are injected, not hardcoded
- [ ] Input is validated
- [ ] Single responsibility principle followed
- [ ] Code is formatted consistently
- [ ] JSDoc comments for public APIs
- [ ] Modern ES6+ features used appropriately
