# GitHub Copilot Best Practices for Enterprise Applications

---

## 1. Governance & Policy Setup

**Establish clear usage policies before rollout.**

- Define which repositories Copilot is enabled on — restrict sensitive or compliance-critical repos if needed.
- Use **GitHub Copilot for Business/Enterprise** licenses to enforce org-level policies via the GitHub Admin console.
- Set content exclusion rules (`copilot_content_exclusions`) to prevent Copilot from reading files containing secrets, PII, or regulated data (e.g., `.env`, HIPAA-related configs).
- Enforce policies through GitHub Organizations: enable/disable Copilot per team or per repository.

---

## 2. Prompt Engineering

**The quality of Copilot's output is directly proportional to the quality of your context.**

- **Write descriptive comments before code**: Copilot uses surrounding context as a prompt.  
  Example: `// Validate JWT token and extract claims, throw UnauthorizedException if invalid`
- **Name variables and functions meaningfully**: `calculateMonthlyInterestRate()` gives Copilot far more signal than `calc()`.
- **Use inline examples**: Show expected input/output patterns in comments when logic is non-trivial.
- **Break complex tasks into smaller prompts**: Scaffold method by method instead of entire classes.

---

## 3. Code Review & Validation

**Never trust Copilot output blindly — treat it as a junior developer's suggestion.**

- Always review generated code for:
  - **Logic correctness**
  - **Security vulnerabilities** (SQL injection, input validation, secrets, deserialization)
  - **License compliance** (use duplication detection filter in Enterprise settings)
- Require **mandatory code review** with branch protection rules.
- Integrate **GitHub Advanced Security (GHAS)**: CodeQL + secret scanning.

---

## 4. Security Hardening

**Copilot follows patterns it sees — guide it toward secure patterns.**

- Maintain `/docs/coding-standards.md` or `.github/copilot-instructions.md` with security baselines.
- Use **Copilot Autofix** with GHAS to suggest fixes for vulnerabilities.
- Configure **content exclusions** for sensitive files (`*.pem`, `*.key`, `*.env`).
- Enable **secret scanning push protection**.

---

## 5. Custom Instructions & Repository Context

**Train Copilot on your enterprise standards.**

- Use `.github/copilot-instructions.md` for:
  - Preferred frameworks/libraries
  - Coding style (e.g., async/await)
  - Architecture patterns (e.g., Clean Architecture, CQRS)
- Use **Copilot Chat context** (`#file`, `#selection`, `#codebase`).
- Use **knowledge bases** (Copilot Enterprise) to ground answers in org standards.

---

## 6. Testing Strategy

**Use Copilot to accelerate test coverage, not skip it.**

- Generate:
  - Unit tests
  - Edge case tests (`null inputs, boundary values, exceptions`)
  - Mock setups
- Validate tests assert meaningful behavior.
- Use Copilot Chat `/tests` command.
- Enforce coverage thresholds in CI.

---

## 7. CI/CD Integration

**Copilot accelerates code; pipelines enforce quality.**

- Keep branch protection rules enforced.
- Gates for Copilot-generated code:
  - Linting (ESLint, Checkstyle, StyleCop)
  - Static analysis (SonarQube, CodeQL)
  - Dependency scanning (Dependabot)
  - Unit + integration tests
- Use **Copilot for Pull Requests** for summaries, but require human-authored descriptions for critical changes.

---

## 8. Developer Training & Enablement

**Copilot is a force multiplier for skilled developers, not a replacement.**

- Train developers on:
  - Prompting techniques
  - Critical evaluation of AI code
  - When NOT to use Copilot (crypto, compliance code)
- Establish **internal prompt libraries**.
- Run **Copilot pairing sessions**.

---

## 9. Audit & Compliance

**Maintain accountability in regulated environments.**

- Use **Copilot usage metrics** in Admin dashboard.
- Reinforce that **developers own committed code**.
- Document Copilot code review/testing in regulated industries.
- Verify GitHub’s privacy commitments: Copilot for Business/Enterprise does not train on snippets.

---

## 10. Feedback Loop & Continuous Improvement

**Treat Copilot adoption as an evolving practice.**

- Collect developer feedback on suggestion quality.
- Expand `.github/copilot-instructions.md` and knowledge bases.
- Monitor for duplication across teams.
- Track metrics: PR cycle time, defect rates, coverage trends.

---

## Summary Table

| Area       | Key Action                                                   |
|------------|--------------------------------------------------------------|
| Governance | Content exclusions, org policies, license enforcement        |
| Prompting  | Descriptive comments, meaningful naming, scoped prompts      |
| Security   | GHAS integration, custom instructions, secret scanning       |
| Testing    | Generate + validate tests, enforce coverage gates            |
| CI/CD      | All quality gates apply regardless of AI assistance          |
| Compliance | Code ownership stays with developer, same audit standards    |
| Training   | Teach critical evaluation, not blind acceptance              |
