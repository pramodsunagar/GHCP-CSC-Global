# GitHub Copilot — Chat Variables

Chat variables (prefixed with `#`) are **context injectors**. They tell Copilot Chat exactly what to analyze when answering your prompt. Without them, responses are generic. With them, responses become precise and codebase-aware.

---

## 1. `#file`

**What it does:** Attaches the **full content of a specific file**.

**Usage:**

```
Explain the authentication flow in #file:AuthService.cs
Does #file:appsettings.json have insecure configurations?
Refactor #file:CustomerRepository.cs to match #file:OrderRepository.cs
```

---

## 2. `#selection`

**What it does:** Uses **currently selected code**.

**Usage:**

```
/explain #selection
What are performance implications of #selection?
Write unit tests for #selection
```

---

## 3. `#codebase`

**What it does:** Searches the **entire workspace**.

**Usage:**

```
How is error handling implemented across #codebase?
Find PaymentGateway usage in #codebase
Are there circular dependencies in #codebase?
```

---

## 4. `#sym`

**What it does:** Targets a **specific symbol** (method/class/interface).

**Usage:**

```
/explain #sym:CalculateTax
Write tests for #sym:OrderService.ProcessRefund
Who implements #sym:IPaymentProvider?
```

---

## 5. `#editor`

**What it does:** Uses the **active editor file**.

**Usage:**

```
Summarize responsibilities of #editor
Are there code smells in #editor?
```

---

## 6. `#terminalLastCommand`

**What it does:** Captures **last terminal command + output**.

**Usage:**

```
Why did #terminalLastCommand fail?
Explain #terminalLastCommand output
```

---

## 7. `#terminalSelection`

**What it does:** Uses **selected terminal output**.

**Usage:**

```
Explain error in #terminalSelection
Resolve dependency conflict in #terminalSelection
```

---

## 8. `#problems`

**What it does:** Pulls **all errors/warnings from Problems panel**.

**Usage:**

```
Fix all issues in #problems
Prioritize #problems by severity
```

---

## 9. `#vscodeAPI`

**What it does:** Loads **VS Code API documentation**.

**Usage:**

```
Using #vscodeAPI, create a status bar item
Register a tree view provider with #vscodeAPI
```

---

## 10. `#testFailure`

**What it does:** Injects **failing test details**.

**Usage:**

```
Why is #testFailure failing?
Fix code to pass #testFailure
```

---

## 11. `#changes`

**What it does:** Includes **current Git changes**.

**Usage:**

```
Review #changes before commit
Write commit message for #changes
```

---

## 12. `#git`

**What it does:** Provides **repository state**.

**Usage:**

```
Summarize recent commits using #git
Suggest branch name based on #git
```

---

## 13. `#extensions`

**What it does:** Lists **installed VS Code extensions**.

**Usage:**

```
Which #extensions support debugging Node.js?
Any conflicts in #extensions?
```

---

## 14. `#output`

**What it does:** Reads **Output panel logs**.

**Usage:**

```
Analyze #output for build issues
Explain warnings in #output
```

---

## 15. `#debugConsole`

**What it does:** Injects **debug session output**.

**Usage:**

```
Why is value incorrect in #debugConsole?
Interpret exception in #debugConsole
```

---

## 16. `#workspace`

**What it does:** Provides **workspace metadata**.

**Usage:**

```
What projects exist in #workspace?
What build system is used in #workspace?
```

---

## 17. `#solution` (.NET)

**What it does:** Provides **.NET solution structure**.

**Usage:**

```
How are projects linked in #solution?
Any circular references in #solution?
```

---

## 18. `#diff`

**What it does:** Injects **Git diff context**.

**Usage:**

```
Review #diff for regressions
Generate release notes from #diff
```

---

## 19. `#newFile`

**What it does:** Creates **new file with suggested structure**.

**Usage:**

```
#newFile Create Product interface with id, name, price
#newFile Generate Dockerfile for .NET API
```

---

## 20. `#copilotEdits`

**What it does:** Tracks **Copilot edit history in session**.

**Usage:**

```
What changed in #copilotEdits?
Continue refactor based on #copilotEdits
```

---

## Quick Reference Table

| Variable               | Scope         | Use Case               |
| ---------------------- | ------------- | ---------------------- |
| `#file`                | File          | File-level analysis    |
| `#selection`           | Code block    | Targeted fixes         |
| `#codebase`            | Repo          | Cross-project insights |
| `#sym`                 | Symbol        | Focused logic          |
| `#editor`              | Active file   | Quick analysis         |
| `#terminalLastCommand` | Terminal      | Debug commands         |
| `#terminalSelection`   | Terminal      | Specific logs          |
| `#problems`            | Errors        | Bulk fixes             |
| `#vscodeAPI`           | Docs          | Extension dev          |
| `#testFailure`         | Tests         | Debug failures         |
| `#changes`             | Git diff      | Pre-commit review      |
| `#git`                 | Repo          | Branch/commit context  |
| `#extensions`          | Tools         | Env insights           |
| `#output`              | Logs          | Build/debug output     |
| `#debugConsole`        | Runtime       | Debugging              |
| `#workspace`           | Project       | Structure              |
| `#solution`            | .NET          | Multi-project context  |
| `#diff`                | Git           | Code review            |
| `#newFile`             | File creation | Scaffolding            |
| `#copilotEdits`        | Session       | Continuity             |

---

## Power Combos

```
# Code review before PR
Review #changes against #file:CONTRIBUTING.md

# Refactoring
Refactor #sym:OrderService using pattern from #file:CustomerService.cs

# Bulk error triage
Categorize #problems into breaking vs warnings

# Debugging
Given #debugConsole and #file:PaymentService.cs, why failure occurs?

# Agent mode execution
Using #codebase, implement JWT refresh logic similar to #file:AuthService.cs
```

---

## Key Insight

> The more precise your context (`#variables`), the better Copilot behaves —
> shifting from a generic assistant to a **codebase-aware senior engineer**.
