# Pass-through method

A **pass-through method** is a method that does nothing except delegate to another method, adding no additional logic, transformation, or value.

## Example

```java
// DAO layer
public class UserDao {
    public User findById(Long id) {
        return database.query("SELECT * FROM users WHERE id = ?", id);
    }
}

// Service layer - pass-through method
public class UserService {
    private UserDao userDao;

    public User findById(Long id) {
        return userDao.findById(id);  // Simply delegates, adds nothing
    }
}
```

## Why they're problematic

Pass-through methods are often considered a code smell because they:

1. **Add unnecessary indirection** - Callers must navigate through extra layers to understand what's happening
2. **Increase code volume without adding value** - More code to read, test, and maintain
3. **Obscure the actual implementation** - The real logic is buried deeper in the call stack
4. **Violate the principle of meaningful abstraction** - Each layer should provide value, not just forward calls

## When they might be acceptable

- **API stability**: Providing a stable interface while the underlying implementation may change
- **Future extensibility**: Placeholder for logic that will be added later (though this is speculative)
- **Interface compliance**: When implementing an interface that requires certain methods

## Better alternatives

If a service layer method only delegates to a DAO, consider:
- Letting callers access the DAO directly (if appropriate for your architecture)
- Adding meaningful logic (validation, logging, caching, transaction management)
- Removing the unnecessary layer entirely
