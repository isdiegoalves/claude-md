# Write Human Code & Don't Over-Engineer

> Prompting Techniques: **Zero-shot** (human code) + **Directional Stimulus** (simplicity)

---

## Part 1: Write Human Code

### The Core Principle

Write code that looks like a human wrote it — not a corporate template generator. Code is communication between people, not just instructions for computers.

### Chain-of-Thought: Why "robotic" code is bad

1. **Increases cognitive load** - Developers waste time decoding obvious comments
2. **Ages poorly** — Explanatory comments go stale; code doesn't lie
3. **Distorts priorities** — Focus on documenting the obvious instead of explaining the complex

---

### Anti-Patterns of Robotic Code

#### ❌ Obvious Corporate Comments

```typescript
/**
 * Button Component
 * This component renders a button element
 * @author Claude
 * @version 1.0
 * @param props - The properties for the button
 * @returns JSX.Element
 */
export const Button: React.FC<ButtonProps> = (props): JSX.Element => {
  // Check if button is disabled
  const isDisabled = props.disabled;

  // Render the button
  return (
    <button disabled={isDisabled}>
      {props.children}
    </button>
  );
};
```

#### ❌ Premature Excessive Separation of Concerns

```typescript
// utils/formatting/date/formatDate.ts
// utils/formatting/date/formatTime.ts
// utils/formatting/date/constants.ts
// utils/formatting/date/types.ts

// For a single date formatting function!
```

#### ❌ Mechanical Naming

```typescript
interface DataInterface {}
class ManagerClass {}
type ConfigType = {}
```

---

### Patterns of Human Code

#### ✅ Comments That Explain the "Why", Not the "What"

```typescript
// ❌ Bad: explains the obvious
// Increment counter by 1
counter++;

// ✅ Good: explains the intention
// We need to adjust the index because arrays at moment X are 0-based
// but the legacy system expects 1-based
counter++;
```

#### ✅ Names That Speak for Themselves

```typescript
// ❌ Bad: needs a comment
function process(d: Data) { /* ... */ } // processes data

// ✅ Good: descriptive name
function normalizeUserProfile(rawProfile: ApiResponse): User {
  /* ... */
}
```

#### ✅ Consistency with Project Patterns

```typescript
// If the project uses:
const user = { name: 'John', age: 30 };

// Don't invent:
const userObj = new UserObject();
userObj.setName('John');
userObj.setAge(30);
```

---

### Directional Stimulus: The Decisive Question

> If three experienced developers would all write it the same way, that's the way it should be written.

---

## Part 2: Don't Over-Engineer

### The Simplicity Principle

**Don't build for imaginary scenarios.** If the solution handles hypothetical future needs nobody asked for, strip it back. Simple and correct beats elaborate and speculative.

### Chain-of-Thought: Signs of Over-Engineering

1. **"What if in the future..."** — You're guessing requirements
2. **Abstractions without concrete use** — Interfaces for "flexibility" that will never be used
3. **Excessive configuration** — Plugin systems for 2 use cases
4. **Premature optimization** — Optimizing code that isn't yet a bottleneck

---

### Anti-Patterns of Over-Engineering

#### ❌ Plugin System for Internal Code

```typescript
// To add ONE email validation?
interface ValidatorPlugin {
  name: string;
  validate: (value: unknown) => ValidationResult;
}

class ValidationRegistry {
  private plugins = new Map<string, ValidatorPlugin>();

  register(plugin: ValidatorPlugin) { /* ... */ }
  validate(field: string, value: unknown) { /* ... */ }
}

// VS
const isEmail = (s: string) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(s);
```

#### ❌ Factory Factories

```typescript
abstract class AbstractFactory<T> {
  abstract create(): T;
}

class ServiceFactory extends AbstractFactory<Service> {
  create() { return new Service(); }
}

// VS
const service = new Service();
```

#### ❌ Extensive Configuration for Default Values

```typescript
const config = {
  database: {
    connection: {
      pool: {
        min: process.env.DB_POOL_MIN ? parseInt(process.env.DB_POOL_MIN) : 2,
        max: process.env.DB_POOL_MAX ? parseInt(process.env.DB_POOL_MAX) : 10,
        timeout: process.env.DB_TIMEOUT ? parseInt(process.env.DB_TIMEOUT) : 30000,
        // ... 20 more options
      }
    }
  }
};
```

---

### Directional Stimulus in Action: Quick Questions

Before adding complexity, ask:

| Question | If the answer is... | Action |
|----------|---------------------|--------|
| Did someone ask for this? | No | Don't implement |
| Will it be used in the next 30 days? | No | Don't implement |
| Would simplifying break something existing? | No | Simplify |
| Would three experienced devs do it this way? | No | Reconsider |

---

### Comparative Examples

#### Scenario: Validate a login form

```typescript
// ❌ Over-Engineered
class ValidationStrategy {
  constructor(private rules: ValidationRule[]) {}

  async execute<T>(data: T): Promise<ValidationResult<T>> {
    const results = await Promise.all(
      this.rules.map(rule => rule.validate(data))
    );
    return this.aggregate(results);
  }

  private aggregate(results: RuleResult[]) { /* ... */ }
}

// ✅ Simple and Direct
function validateLogin(email: string, password: string): string | null {
  if (!email.includes('@')) return 'Invalid email';
  if (password.length < 6) return 'Password too short';
  return null;
}
```

---

## Summary: The Balance

| Aspect | Human Code | Don't Over-Engineer |
|--------|-----------|---------------------|
| **Focus** | Readability | Simplicity |
| **Avoids** | Roboticism | Speculative complexity |
| **Key question** | "Would three devs do it this way?" | "Did anyone ask for this?" |
| **Direction** | Clarity over ceremony | Functional over abstract |

> **Final rule**: Code should be as simple as possible, but no simpler. The intent should be clear on first read.
