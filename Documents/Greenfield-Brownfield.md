# GitHub Copilot — Top 15 Best Practices for Developers

---

## Greenfield vs Brownfield Context

|                  | **Greenfield**                              | **Brownfield**                                        |
| ---------------- | ------------------------------------------- | ----------------------------------------------------- |
| Definition       | Brand new project, no existing code         | Existing/legacy codebase being extended or modernized |
| Copilot Strength | Rapid scaffolding, architecture setup       | Code comprehension, incremental change, refactoring   |
| Primary Risk     | Over-generating boilerplate without thought | Copilot lacking context of existing patterns          |

---

## 1. Set Up Custom Instructions Before Writing a Single Line

**Why it matters:** Copilot generates code based on context. Without instructions, it guesses your conventions.

**Greenfield:** Create `.github/copilot-instructions.md` at project start. Define your stack, patterns, and non-negotiables upfront — before any code exists.

```markdown
# .github/copilot-instructions.md
- Language: TypeScript, strict mode enabled
- Framework: NestJS with Clean Architecture
- ORM: TypeORM with repository pattern
- Always use async/await, never .then()/.catch()
- All API responses must use a standard ApiResponse<T> wrapper
```

**Brownfield:** Reverse-engineer your existing conventions and codify them into the same file. Copilot will then align new suggestions with the legacy style rather than fighting it.

---

## 2. Use Meaningful Naming as a Prompt Signal

**Why it matters:** Copilot uses your variable and function names as implicit prompts. Vague names produce vague code.

**Greenfield:** Establish naming conventions from day one. Descriptive names scaffold entire method bodies correctly.

```typescript
// Weak signal — Copilot guesses intent
async function process(data: any) { }

// Strong signal — Copilot generates correct logic
async function validateAndEnrichCustomerProfile(rawInput: CustomerDto): Promise<EnrichedCustomer> { }
```

**Brownfield:** When extending legacy code with poor naming, add a descriptive comment above the function *before* invoking Copilot — use the comment as your real prompt.

---

## 3. Prompt with Comments First, Accept Code Second

**Why it matters:** Writing the intent before the code forces clarity in your own thinking AND gives Copilot a precise target.

**Greenfield:** Adopt a comment-first workflow as a team standard.

```python
# Connect to PostgreSQL using connection string from environment variable
# Retry up to 3 times with exponential backoff on connection failure
# Raise DatabaseConnectionError if all retries exhausted
def connect_to_database():
```

> Copilot generates the full implementation matching all three requirements.

**Brownfield:** When modifying existing code, add a `// INTENT:` comment above the change location before triggering Copilot suggestions — prevents it from mimicking the old (potentially wrong) surrounding pattern.

---

## 4. Scope Every Prompt — Avoid "Generate Everything"

**Why it matters:** Large, vague prompts produce large, vague code that's hard to validate.

**Greenfield:**

```
// BAD: Build me a full e-commerce checkout service
// GOOD: Write a method to calculate order total including tax and discount codes
```

**Brownfield:** Never ask Copilot to "rewrite this class" in one shot. Break it into: extract interface → implement method → add validation → add tests. Each step is reviewable independently.

---

## 5. Always Review for Security — Never Auto-Accept

**Why it matters:** Copilot learns from public code which includes insecure patterns. It will reproduce them.

**Greenfield:** Build a security checklist into your PR template from day one. Every Copilot-assisted PR must be checked for:

* Hardcoded credentials
* Missing input validation
* SQL/NoSQL injection risks
* Insecure deserialization

**Brownfield:** Legacy codebases already carry security debt. Copilot may replicate existing insecure patterns found nearby. Use **GitHub Advanced Security (CodeQL)** as a safety net and never merge without a scan pass.

```csharp
// Copilot may suggest this (matching legacy pattern around it):
var query = "SELECT * FROM Users WHERE name = '" + name + "'";  // ← SQL Injection

// You must redirect it:
// Use parameterized query with Dapper
var users = await conn.QueryAsync<User>("SELECT * FROM Users WHERE name = @name", new { name });
```

---

## 6. Leverage `#file`, `#sym`, and `#codebase` Chat References

**Why it matters:** Copilot Chat without context gives generic answers. With context, it gives project-specific answers.

**Greenfield:** As your project grows, use `#codebase` in chat to ensure Copilot understands the evolving structure before suggesting new components.

**Brownfield:** This is critical. Legacy code has implicit conventions everywhere. Always reference relevant files:

```
/explain #file:OrderProcessor.cs — what validation rules are already implemented?
/fix #selection — match the error handling style used in #file:CustomerService.cs
/tests #sym:CalculateShippingCost — generate tests consistent with existing test patterns in #file:OrderTests.cs
```

---

## 7. Generate Tests Immediately After Each Method

**Why it matters:** Copilot can generate tests while the implementation intent is still captured in context. Waiting means losing that context.

**Greenfield:** Write the method → immediately run `/tests` → review and commit both together.

**Brownfield:** Use Copilot to backfill tests for untested legacy code. Provide context about expected behavior in your prompt:

```
// This method calculates refund amount, should return 0 if order is older than 30 days,
// full amount if within 7 days, 50% if between 7 and 30 days
/tests
```

---

## 8. Use Copilot to Understand Before You Modify

**Why it matters:** Brownfield failures often come from modifying code without full understanding.

**Brownfield (critical):**

```
/explain #file:LegacyPricingEngine.cs
```

```
What side effects does this method have? 
What other code in #codebase depends on this method's return value?
```

> Build a mental model before making changes to prevent regressions.

---

## 9. Establish a "Copilot Review" Step in Your PR Checklist

**Why it matters:** AI-generated code requires strong human validation.

**Greenfield:**

```markdown
## Copilot Usage
- [ ] Were any Copilot suggestions accepted in this PR?
- [ ] All accepted suggestions reviewed for correctness
- [ ] Security implications checked
- [ ] Generated tests validated
```

**Brownfield:** Add:

* Does Copilot-suggested code respect existing architectural boundaries?

---

## 10. Control What Copilot Can See with Content Exclusions

**Why it matters:** Copilot reads open files for context — sensitive data must be excluded.

```yaml
# .github/copilot_content_exclusions.yml
- "**/.env*"
- "**/secrets/**"
- "**/migrations/**"
- "**/certs/**"
```

**Brownfield:** Audit legacy repos for hidden secrets before enabling Copilot.

---

## 11. Use Copilot for Boilerplate, Humans for Business Logic

**Why it matters:** Copilot is pattern-strong but domain-weak.

**Delegate to Copilot:**

* DTOs, controllers, DI setup, configs, CI/CD

**Keep manual:**

* Business rules, pricing logic, workflows

---

## 12. Validate Generated Dependencies and Versions

**Why it matters:** Suggested packages may be outdated or vulnerable.

```bash
npm audit
dotnet list package --vulnerable
pip-audit
```

**Brownfield checks:**

* Version compatibility
* Dependency conflicts
* Existing alternatives in project

---

## 13. Maintain a Shared Prompt Library for Your Team

**Why it matters:** Good prompts are reusable assets.

```markdown
## Useful Copilot Prompts

### Generate API Controller
Create a NestJS controller with CRUD endpoints using ApiResponse<T> and JwtAuthGuard

### EF Core Migration
Add migration to include new column with default value
```

---

## 14. Use Copilot to Accelerate Refactoring, Not Avoid It

**Why it matters:** Copilot can amplify both good and bad code.

**Example:**

```
/fix — ensure this follows repository pattern like #file:CustomerRepository.cs
```

**Brownfield planning:**

```
Suggest how to split this class using Single Responsibility Principle.
Reference #file:OrderManager.cs
```

---

## 15. Treat Copilot as a Pair Programmer, Not Autocomplete

**Why it matters:** Passive use leads to poor code quality.

**Engage actively:**

```
What are trade-offs between CQRS and direct service calls?
What breaks if I change return type of GetShippingRate()?
```

> Stay in control: direct, review, validate.

---

## Summary Matrix

| #  | Best Practice            | Greenfield Priority   | Brownfield Priority         |
| -- | ------------------------ | --------------------- | --------------------------- |
| 1  | Custom Instructions      | 🔴 Critical           | 🔴 Critical                 |
| 2  | Meaningful Naming        | 🔴 Foundational       | 🟡 Compensate with comments |
| 3  | Comment-First Prompting  | 🔴 Core               | 🔴 Essential                |
| 4  | Scope Prompts            | 🟡 Good habit         | 🔴 Critical                 |
| 5  | Security Review          | 🔴 Mandatory          | 🔴 Mandatory                |
| 6  | Context References       | 🟡 Growing importance | 🔴 Essential                |
| 7  | Tests Generation         | 🔴 Early habit        | 🔴 Backfill                 |
| 8  | Understand First         | 🟢 Lower              | 🔴 Critical                 |
| 9  | PR Checklist             | 🔴 Required           | 🔴 Required                 |
| 10 | Content Exclusions       | 🔴 Early setup        | 🔴 Audit required           |
| 11 | Boilerplate vs Logic     | 🔴 Define early       | 🔴 Protect domain           |
| 12 | Dependency Validation    | 🔴 Always             | 🔴 Critical                 |
| 13 | Prompt Library           | 🟡 Build gradually    | 🔴 Capture legacy patterns  |
| 14 | Refactoring Discipline   | 🟡 Enforce            | 🔴 Essential                |
| 15 | Pair Programming Mindset | 🔴 Cultural           | 🔴 Mandatory                |

---

🔴 Critical    🟡 Important    🟢 Lower Risk
