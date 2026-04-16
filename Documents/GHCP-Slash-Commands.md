# GitHub Copilot — Slash Commands

Slash commands are **intent signals** — they instruct Copilot *how* to respond, not just *what* to answer. Combine them with `#` chat variables for precise, context-aware results.

---

## 1. `/explain`

**What it does:** Explains code logic, flow, and purpose in plain English.

**Works in:** VS Code, GitHub.com, Mobile

```id="sc1"
/explain
/explain #file:JwtTokenService.cs
/explain what is the retry strategy in #selection?
```

---

## 2. `/fix`

**What it does:** Detects and fixes bugs or errors.

**Works in:** VS Code, GitHub.com

```id="sc2"
/fix
/fix #selection — ensure null safety
/fix #problems — resolve all issues
```

---

## 3. `/tests`

**What it does:** Generates unit tests.

**Works in:** VS Code, GitHub.com

```id="sc3"
/tests
/tests #sym:CalculateOrderTotal with edge cases
/tests #file:DiscountService.cs using xUnit
```

---

## 4. `/doc`

**What it does:** Generates documentation comments.

```id="sc4"
/doc
/doc #selection — include param and exception docs
/doc #file:CustomerService.cs for all public methods
```

---

## 5. `/optimize`

**What it does:** Improves performance and efficiency.

```id="sc5"
/optimize
/optimize #selection — reduce complexity
/optimize #file:ReportGenerator.cs for memory usage
```

---

## 6. `/simplify`

**What it does:** Simplifies complex code for readability.

```id="sc6"
/simplify
/simplify #selection — reduce nesting
/simplify #sym:ValidateUserInput
```

---

## 7. `/review`

**What it does:** Performs a code review.

```id="sc7"
/review
/review #selection — check design issues
/review #changes — pre-commit validation
```

---

## 8. `/new`

**What it does:** Scaffolds new components/files.

```id="sc8"
/new React ProductCard component
/new .NET API with CRUD endpoints
/new GitHub Actions workflow
```

---

## 9. `/newNotebook`

**What it does:** Creates Jupyter Notebook.

```id="sc9"
/newNotebook analyze CSV with pandas and visualize
/newNotebook build ML classification model
```

---

## 10. `/terminal`

**What it does:** Suggests terminal commands.

```id="sc10"
/terminal delete .log files older than 7 days
/terminal create git branch feature/payment-refactor
```

---

## 11. `/search`

**What it does:** Generates workspace search queries.

```id="sc11"
/search all HttpException usage
/search classes implementing IRepository
```

---

## 12. `/api`

**What it does:** Provides VS Code API guidance.

```id="sc12"
/api register a WebviewPanel
/api create a custom tree view
```

---

## 13. `/startDebugging`

**What it does:** Generates debug configuration.

```id="sc13"
/startDebugging Node.js API on port 3000
/startDebugging attach to .NET process in Docker
```

---

## 14. `/setupTests`

**What it does:** Sets up testing frameworks.

```id="sc14"
/setupTests add Jest to React project
/setupTests configure xUnit with Moq
```

---

## 15. `/fixTestFailure`

**What it does:** Fixes failing tests.

```id="sc15"
/fixTestFailure
/fixTestFailure #testFailure
```

---

## 16. `/clear`

**What it does:** Clears chat context.

```id="sc16"
/clear
```

---

## 17. `/help`

**What it does:** Shows available commands.

```id="sc17"
/help
/help what chat variables exist?
```

---

## 18. `/runCommand`

**What it does:** Executes VS Code commands.

```id="sc18"
/runCommand open terminal split view
/runCommand format document
```

---

## 19. `/feedback`

**What it does:** Submits feedback.

```id="sc19"
/feedback this suggestion was incorrect
/feedback test generation was excellent
```

---

## 20. `/commit`

**What it does:** Generates commit messages.

```id="sc20"
/commit
/commit #changes using conventional commits
/commit #diff with detailed explanation
```

---

## Complete Reference Table

| #  | Command           | Purpose              | Works In                |
| -- | ----------------- | -------------------- | ----------------------- |
| 1  | `/explain`        | Explain code         | VS Code, GitHub, Mobile |
| 2  | `/fix`            | Fix errors           | VS Code, GitHub         |
| 3  | `/tests`          | Generate tests       | VS Code, GitHub         |
| 4  | `/doc`            | Documentation        | VS Code, GitHub         |
| 5  | `/optimize`       | Performance          | VS Code, GitHub         |
| 6  | `/simplify`       | Readability          | VS Code                 |
| 7  | `/review`         | Code review          | VS Code, GitHub         |
| 8  | `/new`            | Scaffold code        | VS Code, GitHub         |
| 9  | `/newNotebook`    | Notebook creation    | VS Code                 |
| 10 | `/terminal`       | Terminal commands    | VS Code                 |
| 11 | `/search`         | Code search          | VS Code                 |
| 12 | `/api`            | VS Code API          | VS Code                 |
| 13 | `/startDebugging` | Debug config         | VS Code                 |
| 14 | `/setupTests`     | Test setup           | VS Code                 |
| 15 | `/fixTestFailure` | Fix tests            | VS Code                 |
| 16 | `/clear`          | Reset chat           | All                     |
| 17 | `/help`           | Help guide           | VS Code, GitHub         |
| 18 | `/runCommand`     | Run VS Code commands | VS Code                 |
| 19 | `/feedback`       | Submit feedback      | VS Code                 |
| 20 | `/commit`         | Commit messages      | VS Code, GitHub         |

---

## High-Impact Command Combos

```bash id="combos"
# Pre-commit
/review #changes → /commit #changes

# TDD workflow
/tests #sym:ProcessRefund → /fixTestFailure → /optimize #selection

# Bug triage
/explain #terminalLastCommand → /fix #problems → /review #changes

# New feature
/new → /tests → /doc → /commit

# Legacy code
/explain #file:LegacyService.cs → /simplify → /review

# Debug loop
/explain #testFailure → /fixTestFailure → /tests
```

---

## Pro Tip — Combine Commands with Context

```id="tip"
/fix #selection
/tests #sym:MethodName in style of #file:ExistingTests.cs
/review #changes against #file:CONTRIBUTING.md
/optimize #selection — target O(n)
/commit #changes using conventional commits
```

---

## Key Insight

> A slash command defines **intent**.
> A `#` variable defines **context**.
> Together, they produce **precision-level Copilot output**.
