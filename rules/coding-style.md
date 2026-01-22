# Coding Style

## Immutability (CRITICAL)

ALWAYS create new objects, NEVER mutate:

```typescript
// WRONG: Mutation
function updateUser(user: User, name: string): User {
  user.name = name; // MUTATION!
  return user;
}

// CORRECT: Immutability
function updateUser(user: User, name: string): User {
  return { ...user, name };
}
```

## File Organization

MANY SMALL FILES > FEW LARGE FILES:

- High cohesion, low coupling
- 200-400 lines typical, 800 max
- Extract utilities from large components

**Organize by feature/domain, not by type:**

```
BAD:  /components, /utils, /services
GOOD: /features/auth, /features/dashboard, /shared/ui
```

## Error Handling

ALWAYS handle errors comprehensively:

```typescript
try {
  const result = await riskyOperation();
  return result;
} catch (error) {
  // Use structured logging in production
  logger.error("Operation failed:", { error, context });
  throw new Error("Detailed user-friendly message");
}
```

## Input Validation

ALWAYS validate user input:

```typescript
import { z } from "zod";

const UserSchema = z.object({
  email: z.string().email(),
  age: z.number().int().min(0).max(150),
});

const validated = UserSchema.parse(input);
```

## Code Quality Checklist

Before marking work complete:

- [ ] Code is readable and well-named
- [ ] Functions are small (<50 lines)
- [ ] Files are focused (<800 lines)
- [ ] No deep nesting (>4 levels)
- [ ] Proper error handling with logging
- [ ] No console.log (use logger)
- [ ] No hardcoded values (use config/env)
- [ ] No mutation (immutable patterns used)
