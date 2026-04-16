# GitHub Copilot — Ask, Agent & Plan Modes

---

## Overview

These three modes define **how Copilot interacts with you and your codebase**. Choosing the right mode directly impacts the quality, safety, and autonomy of the outcome.

| Mode      | Nature               | Autonomy                         | Best For                        |
| --------- | -------------------- | -------------------------------- | ------------------------------- |
| **Ask**   | Conversational Q&A   | None — you act                   | Questions, explanations, advice |
| **Plan**  | Structured strategy  | Low — Copilot plans, you approve | Complex multi-step changes      |
| **Agent** | Autonomous execution | High — Copilot acts              | End-to-end task completion      |

---

## Ask Mode

### What It Is

A **conversational interface** where you ask Copilot questions and receive explanations, suggestions, or code snippets. Copilot does **not** modify files — it only advises.

### How It Works

* You type a question in Copilot Chat
* Copilot reads open files, selections, or attached context
* It responds with explanations, code, or recommendations
* **You manually apply** any changes

### Characteristics

* Zero side effects — no automatic code changes
* Ideal for learning, debugging, and exploration
* Works best with `#file`, `#selection`, `#sym`
* Context improves quality of answers

---

### Real-World Scenarios — Ask Mode

#### Scenario 1 — Onboarding to a Legacy Codebase

```id="ask1"
/explain #file:OrderFulfillmentService.java
What business rules are encoded in this class and what downstream services does it call?
```

> Produces a structured explanation of logic and dependencies.

---

#### Scenario 2 — Architectural Decision Support

```id="ask2"
What are the trade-offs between using Azure Service Bus pub/sub vs direct REST 
API calls for order status notifications in a high-throughput system?
```

> Returns comparative analysis with scalability and reliability considerations.

---

#### Scenario 3 — Debugging a Production Issue

```id="ask3"
Given this stack trace and #file:PaymentProcessor.cs, 
what is the most likely cause of this NullReferenceException at line 87?
```

> Identifies root cause and explains failure conditions.

---

#### Scenario 4 — Code Review Preparation

```id="ask4"
Summarize the changes in #file:CustomerRepository.cs — 
what problem is this solving and any edge cases missed?
```

---

#### Scenario 5 — Compliance Check

```id="ask5"
Does logging in #file:AuditLogger.cs expose sensitive data?
How can it be made compliant?
```

---

## Plan Mode

### What It Is

Plan mode generates a **step-by-step execution plan** before making any changes. You review and approve the plan first.

### How It Works

* You define a complex task
* Copilot analyzes the codebase
* It generates an ordered plan (files, changes, sequence)
* You review/edit/approve
* Execution starts only after approval

### Characteristics

* Reduces risk for large changes
* Forces clarity before execution
* Ideal for multi-file or architectural changes
* Creates alignment between intent and implementation

---

### Real-World Scenarios — Plan Mode

#### Scenario 1 — Feature Across Layers

```id="plan1"
Plan how to add a discountCode field across DB, API, validation, service, and frontend.
```

**Example Plan Output:**

```id="plan1out"
1. Add column to Orders table (migration)
2. Update Order entity
3. Update DTOs
4. Add validation rules
5. Update service logic
6. Update UI
7. Add tests
```

---

#### Scenario 2 — Library Migration

```id="plan2"
Plan migration from Newtonsoft.Json to System.Text.Json across this project.
```

> Identifies impacted files and breaking changes.

---

#### Scenario 3 — Refactoring a Large Class

```id="plan3"
Plan decomposition of UserManager.cs into smaller services while preserving public interfaces.
```

---

#### Scenario 4 — New Microservice Setup

```id="plan4"
Plan scaffold for a new .NET microservice following Clean Architecture from #file:OrderService/Program.cs
```

---

## Agent Mode

### What It Is

Agent mode enables **autonomous, multi-step execution**. Copilot performs actions across files, terminal, and tests with minimal intervention.

### How It Works

* You give a high-level goal
* Copilot decomposes tasks automatically
* Reads files, edits code, runs commands
* Fixes errors iteratively
* Continues until completion or blocker

### Characteristics

* High autonomy
* Executes across editor + terminal
* Self-corrects using errors/logs
* Best for well-defined end-to-end tasks

---

### Real-World Scenarios — Agent Mode

#### Scenario 1 — End-to-End Feature

```id="agent1"
Add JWT auth to Express API, protect routes, add login/refresh endpoints, and tests.
```

**Agent Actions:**

* Installs dependencies
* Creates middleware
* Updates routes
* Runs tests and fixes failures

---

#### Scenario 2 — Fix CI Build

```id="agent2"
Fix failing CI build using #file:build.log and ensure tests pass.
```

---

#### Scenario 3 — Database Evolution

```id="agent3"
Add Status enum to Customer, update queries, tests, and seed data.
```

---

#### Scenario 4 — Code Quality Refactor

```id="agent4"
Refactor methods with cyclomatic complexity > 10 in #file:src/services/
```

---

#### Scenario 5 — Microservice Scaffold

```id="agent5"
Scaffold production-ready .NET microservice with Clean Architecture and Docker support.
```

---

## Choosing the Right Mode

```
Is this a question or understanding problem?
→ ASK MODE

Is this a multi-step change needing approval?
→ PLAN MODE

Is this a well-defined task to execute fully?
→ AGENT MODE
```

---

## Decision Guide

| Situation                         | Mode  |
| --------------------------------- | ----- |
| Understand code                   | Ask   |
| Security / architecture questions | Ask   |
| Multi-file feature with review    | Plan  |
| Library migration                 | Plan  |
| Large refactor                    | Plan  |
| End-to-end feature implementation | Agent |
| Fix CI/CD issues                  | Agent |
| Scaffold new service              | Agent |

---

## Key Principle

> **Ask** → Understand
> **Plan** → Align
> **Agent** → Execute

For complex workflows:

1. Use **Ask** to explore and understand
2. Use **Plan** to define approach
3. Use **Agent** to execute

This progression ensures **control, clarity, and efficiency** when working with GitHub Copilot.
