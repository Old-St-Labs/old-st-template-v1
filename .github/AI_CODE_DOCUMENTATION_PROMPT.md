# AI Code Documentation Prompt

## Purpose
This guide helps AI assistants and developers create **meaningful, maintainable documentation** that adds value without creating visual clutter. Use this as a reference when requesting code documentation.

---

## Core Philosophy

> **"Document interfaces and intentions, not implementations and obvious facts."**

- **Best code is self-documenting** - Prioritize clear naming over comments
- **Comments explain WHY, code shows HOW** - Focus on reasoning, not mechanics
- **Less is more** - Each comment should earn its place
- **Maintenance matters** - Only write comments you're willing to keep updated

---

## Documentation Decision Tree

### 🟢 ALWAYS Document

1. **Public APIs & Interfaces**
   - All exported functions, classes, methods
   - Parameters, return types, exceptions
   - Usage examples for complex APIs

2. **Complex Business Logic**
   - Non-trivial algorithms
   - Business rules and constraints
   - Domain-specific calculations

3. **Non-Obvious Decisions**
   - Why you chose this approach over alternatives
   - Performance trade-offs
   - Security considerations

4. **Gotchas & Edge Cases**
   - Unexpected behavior
   - Known limitations
   - Important preconditions

5. **External Dependencies**
   - Third-party API quirks
   - Integration assumptions
   - Version-specific workarounds

### 🟡 SOMETIMES Document

6. **Helper Functions**
   - Only if behavior is non-obvious from name
   - When side effects exist
   - When performance characteristics matter

7. **Configuration & Constants**
   - Why this specific value was chosen
   - Context for magic numbers

8. **Temporary Code**
   - TODO/FIXME with ticket number and owner
   - Deprecation warnings with timeline

### 🔴 NEVER Document

9. **Obvious Operations**
   - Simple getters/setters
   - Variable assignments
   - Standard patterns

10. **What the Code Already Says**
    - Don't repeat type information available in types
    - Don't describe the code line-by-line
    - Don't state the obvious

11. **Outdated Information**
    - Remove obsolete comments immediately
    - Delete commented-out code (use Git instead)

---

## Language-Specific Templates

### JavaScript/TypeScript (JSDoc)

```javascript
/**
 * [One-line summary in imperative mood]
 * 
 * [Optional: Extended description explaining context, 
 * important behaviors, or usage patterns]
 * 
 * @param {Type} paramName - Description (what it's for, constraints)
 * @param {Type} [optionalParam] - Optional parameter description
 * @returns {Type} Description of return value
 * @throws {ErrorType} When/why this error occurs
 * 
 * @example
 * // Show typical usage
 * const result = functionName(arg1, arg2);
 */
```

**Minimal Documentation (simple functions):**
```javascript
/** Calculates the total price including tax. */
function calculateTotal(price, taxRate) {
    return price * (1 + taxRate);
}
```

### Python (Docstrings)

```python
def function_name(param1: Type, param2: Type) -> ReturnType:
    """One-line summary (imperative mood, ends with period).
    
    Extended description if needed. Explain context,
    behavior, or important considerations.
    
    Args:
        param1: Description of param1 (constraints, format)
        param2: Description of param2
        
    Returns:
        Description of return value
        
    Raises:
        ValueError: When invalid input provided
        
    Example:
        >>> function_name(arg1, arg2)
        expected_output
    """
```

---

## Implementation Comments (Inline)

Use `//` or `#` comments sparingly for:

### ✅ Good Inline Comments

```javascript
// WORKAROUND: IE11 doesn't support Array.from() - remove after IE11 EOL (Dec 2026)
const array = [...nodeList];

// Performance: Binary search because dataset can exceed 1M items
const index = binarySearch(data, target);

// SECURITY: Must validate on server too - client validation is for UX only
if (!isValidEmail(email)) return;

// Business Rule: 30-day grace period per contract §4.2
const GRACE_PERIOD_DAYS = 30;

// TODO(username): Refactor to use new AuthService (ticket #1234)
```

### ❌ Bad Inline Comments

```javascript
// BAD: States the obvious
i++; // Increment i

// BAD: Repeats the code
const user = new User(); // Create new user

// BAD: Outdated information
// This uses MySQL (NOTE: Actually using PostgreSQL now)

// BAD: Should be refactored instead
// This is a complicated function that does multiple things
function doEverything() { ... }
```

---

## AI Documentation Request Template

When asking AI to document code, use this template:

```
Please document this code following these guidelines:

1. SCOPE: [Choose one]
   - [ ] Public API only (external consumers)
   - [ ] Public API + complex internals
   - [ ] Minimal (only non-obvious parts)
   - [ ] Comprehensive (including edge cases)

2. FOCUS ON:
   - [ ] Why this approach was chosen
   - [ ] Edge cases and gotchas
   - [ ] Performance characteristics
   - [ ] Security considerations
   - [ ] Usage examples
   - [ ] Integration notes

3. SKIP:
   - [x] Obvious operations
   - [x] Type information (already in types)
   - [x] Line-by-line descriptions

4. STYLE:
   - Language: [JavaScript/TypeScript/Python]
   - Format: [JSDoc/Docstring]
   - Verbosity: [Minimal/Moderate/Detailed]

[CODE BLOCK HERE]
```

---

## Quality Checklist

Before finalizing documentation, verify:

- [ ] **Adds Value**: Would removing it lose important information?
- [ ] **Stays Current**: Can it be easily maintained?
- [ ] **Avoids Redundancy**: Doesn't repeat type system or obvious code?
- [ ] **Proper Grammar**: Capitalized, punctuated correctly?
- [ ] **Examples Work**: If included, are they tested/valid?
- [ ] **Explains WHY**: Focuses on reasoning, not mechanics?
- [ ] **Appropriate Level**: Matches the visibility (public vs. private)?

---

## Documentation Levels by Code Type

| Code Type | Documentation Level | Focus |
|-----------|-------------------|-------|
| Public API | Comprehensive | Contract, parameters, examples, exceptions |
| Library/Framework | Comprehensive | Usage, patterns, edge cases |
| Application Code | Selective | Business logic, non-obvious decisions |
| Internal Helpers | Minimal | Only if complex or has side effects |
| Tests | Minimal | Test name should be descriptive |
| Scripts/Tools | Moderate | Purpose, usage, requirements |

---

## Examples: Before & After

### ❌ Over-Documented

```javascript
/**
 * Gets the user's first name
 * @param {User} user - The user object
 * @returns {string} The first name of the user
 */
function getFirstName(user) {
    /** Return the firstName property from user */
    return user.firstName; // Returns firstName
}
```

### ✅ Appropriately Documented

```javascript
function getFirstName(user) {
    return user.firstName;
}
```

---

### ❌ Under-Documented

```javascript
function process(data, opts) {
    const result = data.map(x => x * 2.5 + opts.base).filter(x => x > opts.min);
    if (opts.cache) store.set(hash(data), result);
    return result;
}
```

### ✅ Appropriately Documented

```javascript
/**
 * Applies pricing transformation with optional caching.
 * 
 * Formula: (value * 2.5) + base, filtered by minimum threshold.
 * Results are cached when opts.cache=true to avoid recomputation
 * for expensive datasets (>10k items).
 * 
 * @param {number[]} data - Raw values to transform
 * @param {Object} opts - Configuration options
 * @param {number} opts.base - Base amount added to each value
 * @param {number} opts.min - Minimum threshold for filtering
 * @param {boolean} [opts.cache=false] - Enable result caching
 * @returns {number[]} Transformed and filtered values
 */
function process(data, opts) {
    const result = data.map(x => x * 2.5 + opts.base).filter(x => x > opts.min);
    if (opts.cache) store.set(hash(data), result);
    return result;
}
```

---

## Common Patterns

### Constructor Documentation
```javascript
/**
 * Creates an instance of PaymentProcessor.
 * 
 * @param {string} apiKey - Stripe API key
 * @param {Object} [options] - Configuration options
 * @param {number} [options.timeout=5000] - Request timeout in ms
 * @param {boolean} [options.sandbox=false] - Use sandbox environment
 */
constructor(apiKey, options = {}) { ... }
```

### Async Function Documentation
```javascript
/**
 * Fetches user profile with retry logic.
 * 
 * Retries up to 3 times with exponential backoff.
 * Throws if all attempts fail.
 * 
 * @async
 * @param {string} userId - User identifier
 * @returns {Promise<UserProfile>} User profile data
 * @throws {NetworkError} If all retry attempts fail
 * @throws {NotFoundError} If user doesn't exist
 */
async function fetchUserProfile(userId) { ... }
```

### Class Documentation
```javascript
/**
 * Manages user session lifecycle.
 * 
 * Handles authentication tokens, refresh logic, and
 * automatic session renewal. Tokens are stored in
 * memory only (not persisted).
 * 
 * @example
 * const session = new SessionManager(config);
 * await session.login(credentials);
 * const isValid = session.isAuthenticated();
 */
class SessionManager { ... }
```

---

## Key Reminders

1. **Self-documenting code beats comments** - Refactor before documenting
2. **Types reduce documentation needs** - Use TypeScript/type hints
3. **Update or delete** - Outdated docs are harmful
4. **Examples over prose** - Show, don't just tell
5. **Context matters** - Public API needs more docs than internals
6. **Test your examples** - Ensure documented code actually works
7. **Link to external docs** - For standards, algorithms, specifications

---

## References

- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html#jsdoc)
- [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- [PEP 257 - Docstring Conventions](https://peps.python.org/pep-0257/)
- [JSDoc Documentation](https://jsdoc.app/)

---

**Last Updated:** January 2026  
**Version:** 1.0
