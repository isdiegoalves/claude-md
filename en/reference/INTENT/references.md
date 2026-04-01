# Follow References, Not Descriptions

> Technique: **Few-shot Prompting** - Learning from examples/references

---

## The Principle

When the user points to existing code as a reference:
1. **Study thoroughly** before building
2. **Match patterns exactly** - don't reinvent
3. **Working code > English description**

---

## Few-shot via Reference

### How to Learn from Existing Code

```typescript
// EXAMPLE (provided reference):
// Existing UserService.ts
export class UserService {
  async getUser(id: string): Promise<User> {
    const response = await this.api.get(`/users/${id}`);
    return response.data;
  }
}

// TASK: Create ProductService

// ✅ CORRECT - Follows reference pattern:
export class ProductService {
  async getProduct(id: string): Promise<Product> {
    const response = await this.api.get(`/products/${id}`);
    return response.data;
  }
}

// ❌ WRONG - Invents a different pattern:
export const fetchProduct = async (id: string) => {
  return axios.get(`/api/products/${id}`);
};
```

---

## Reference Checklist

Before implementing:
- [ ] Studied the reference code completely
- [ ] Identified the patterns used
- [ ] Noted naming conventions
- [ ] Observed file structure
- [ ] Replicated the patterns in the new implementation

---

## Reference Signals

| Signal | Meaning | Action |
|--------|---------|--------|
| "Like in [file]" | Use as model | Read and follow the pattern |
| "Following the pattern of..." | Required consistency | Study the reference |
| "Similar to [function]" | Controlled adaptation | Copy structure, adapt logic |
| "In the project style" | Existing conventions | Analyze multiple examples |

---

## Few-shot in Action Example

```markdown
User: "Create a new useAuth hook, following the useUser pattern"

Few-shot Action:
1. Read useUser.ts completely
2. Note:
   - Structure: export function useUser() { ... }
   - Return: { user, loading, error }
   - Internals: useState, useEffect, try/catch
3. Replicate structure in useAuth.ts:
   - export function useAuth() { ... }
   - Return: { auth, loading, error }
   - Same state management pattern
```
