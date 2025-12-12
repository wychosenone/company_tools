# Code Review Checklist

## Security

### Injection Vulnerabilities
- [ ] SQL queries use parameterized statements, not string concatenation
- [ ] User input is sanitized before use in shell commands
- [ ] Template rendering escapes user input to prevent XSS
- [ ] File paths are validated to prevent path traversal attacks
- [ ] Regular expressions are safe from ReDoS attacks

### Authentication and Authorization
- [ ] Passwords are hashed using strong algorithms (bcrypt, argon2)
- [ ] Session tokens are generated with cryptographically secure randomness
- [ ] Authorization checks are performed on every protected endpoint
- [ ] Sensitive operations require re-authentication
- [ ] JWT tokens have appropriate expiration times

### Data Protection
- [ ] Sensitive data is encrypted at rest and in transit
- [ ] API keys and secrets are not hardcoded in source code
- [ ] Logs do not contain sensitive information (passwords, tokens, PII)
- [ ] Error messages do not expose internal system details
- [ ] HTTPS is enforced for all external communications

---

## Performance

### Algorithmic Complexity
- [ ] No unnecessary O(n^2) or worse algorithms in hot paths
- [ ] Large data sets are processed with pagination or streaming
- [ ] Recursive functions have proper termination conditions
- [ ] Memoization is used where appropriate for expensive calculations

### Resource Management
- [ ] Database connections are properly pooled and released
- [ ] File handles are closed after use (using try-finally or context managers)
- [ ] Memory-intensive operations are optimized or batched
- [ ] Large objects are not held in memory longer than necessary

### Database Queries
- [ ] N+1 query problems are avoided (use eager loading)
- [ ] Appropriate indexes exist for frequently queried columns
- [ ] Large result sets are paginated
- [ ] Transactions are used appropriately and kept short

### Caching
- [ ] Frequently accessed, rarely changed data is cached
- [ ] Cache invalidation strategy is clearly defined
- [ ] Cache keys are unique and collision-free

---

## Correctness

### Logic Errors
- [ ] Boundary conditions are handled correctly (off-by-one errors)
- [ ] Null/undefined values are checked before use
- [ ] Boolean conditions use correct operators (== vs ===, and vs or)
- [ ] Numeric comparisons account for floating-point precision issues
- [ ] State mutations do not cause race conditions

### Edge Cases
- [ ] Empty collections are handled gracefully
- [ ] Zero and negative values are handled where applicable
- [ ] Unicode and special characters are processed correctly
- [ ] Time zones and daylight saving time are considered
- [ ] Leap years are handled in date calculations

### Concurrency
- [ ] Shared resources are properly synchronized
- [ ] Deadlock potential is analyzed and mitigated
- [ ] Thread-safe data structures are used where needed
- [ ] Async operations have proper error handling

---

## Readability

### Naming Conventions
- [ ] Variable names clearly describe their purpose
- [ ] Function names describe the action being performed
- [ ] Class names are nouns that represent the entity
- [ ] Constants use UPPER_SNAKE_CASE
- [ ] Abbreviations are avoided unless universally understood

### Code Structure
- [ ] Functions do one thing and do it well (Single Responsibility)
- [ ] Function length is reasonable (generally under 30 lines)
- [ ] Nesting depth is minimized (maximum 3-4 levels)
- [ ] Related code is grouped together
- [ ] Magic numbers are replaced with named constants

### Comments and Documentation
- [ ] Complex algorithms have explanatory comments
- [ ] Public APIs have documentation describing usage
- [ ] TODO comments include context and tracking information
- [ ] Comments explain "why" not "what"
- [ ] Outdated comments are removed or updated

---

## Error Handling

### Exception Management
- [ ] Exceptions are caught at appropriate levels
- [ ] Specific exceptions are caught rather than generic catch-all
- [ ] Exceptions are logged with sufficient context
- [ ] Resources are cleaned up even when exceptions occur
- [ ] Error messages are helpful for debugging

### Input Validation
- [ ] All external input is validated before processing
- [ ] Validation errors return clear, actionable messages
- [ ] Type checking is performed where language allows
- [ ] Range and format constraints are enforced
- [ ] Required fields are verified to be present

### Graceful Degradation
- [ ] Network failures are handled with retries or fallbacks
- [ ] Timeouts are set for external service calls
- [ ] Circuit breakers prevent cascade failures
- [ ] Users see friendly error pages, not stack traces

---

## Maintainability

### Code Organization
- [ ] Code follows the project's established patterns
- [ ] Dependencies are injected rather than hardcoded
- [ ] Configuration is externalized from code
- [ ] Feature flags are used for gradual rollouts
- [ ] Dead code is removed

### Testing
- [ ] Unit tests cover critical business logic
- [ ] Edge cases are tested
- [ ] Tests are independent and can run in any order
- [ ] Test names clearly describe what is being tested
- [ ] Mocks are used appropriately without over-mocking

### Version Control
- [ ] Commits are atomic and focused on single changes
- [ ] Commit messages are descriptive and follow conventions
- [ ] Large changes are broken into reviewable chunks
- [ ] Merge conflicts are resolved cleanly

---

## Language-Specific Checks

### Python
- [ ] Type hints are used for function signatures
- [ ] Context managers (with statements) are used for resources
- [ ] List comprehensions are preferred over map/filter where readable
- [ ] f-strings are used for string formatting
- [ ] Virtual environments are used for dependency isolation

### JavaScript/TypeScript
- [ ] const and let are used instead of var
- [ ] Async/await is preferred over raw promises where appropriate
- [ ] Strict equality (===) is used instead of loose equality (==)
- [ ] TypeScript types are specific, not overusing 'any'
- [ ] Optional chaining (?.) is used for nullable access

### Java
- [ ] Resources are managed with try-with-resources
- [ ] Optional is used instead of null for absent values
- [ ] Streams are used for collection processing where appropriate
- [ ] Immutable objects are preferred where possible
- [ ] Equals and hashCode are overridden consistently

### Go
- [ ] Errors are explicitly checked and not ignored
- [ ] Defer is used for cleanup operations
- [ ] Context is passed for cancellation and timeouts
- [ ] Goroutines are properly synchronized
- [ ] Interface segregation is followed

### Rust
- [ ] Ownership rules are followed without unnecessary cloning
- [ ] Error handling uses Result types appropriately
- [ ] Unsafe blocks are minimized and documented
- [ ] Lifetimes are explicit where compiler cannot infer
- [ ] Clippy warnings are addressed

### C/C++
- [ ] Memory allocations have corresponding deallocations
- [ ] Buffer sizes are checked before operations
- [ ] RAII is used for resource management in C++
- [ ] Pointers are checked for null before dereferencing
- [ ] Smart pointers are preferred over raw pointers in C++
