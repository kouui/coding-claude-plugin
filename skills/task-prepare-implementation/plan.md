# Plan: [Task Title]

> **Task:** [link to task.md]
> **Owner:** [name]
> **Created:** YYYY-MM-DD
> **Target Completion:** YYYY-MM-DD

---
 
## 0. Context
 
> **Objective:** [One sentence copied or paraphrased from task.md]
> **Full spec:** [link to task.md]
>
> This plan describes *how* to achieve the above objective.
> For requirements and acceptance criteria, refer to the task.

---

## 1. Overall Architecture

_Describe the high-level architecture of the solution. Include how new components fit into the existing system._

### System Overview

```
[ASCII diagram or description of component relationships]

  ┌──────────┐     ┌──────────┐     ┌──────────┐
  │ Module A  │────▶│ Module B  │────▶│ Module C  │
  └──────────┘     └──────────┘     └──────────┘
```

### Key Components

| Component | Responsibility | New / Modified |
|-----------|---------------|----------------|
| ...       | ...           | New            |
| ...       | ...           | Modified       |

### Data Flow

_How data moves through the system for the primary use case._

1. ...
2. ...
3. ...

---

## 2. Implementation Phases

### Phase 1: [Foundation / Setup]

> **Goal:** _What this phase achieves_
> **Estimated Effort:** X days

- [ ] Step 1.1 — description
- [ ] Step 1.2 — description
- [ ] Step 1.3 — description

**Phase 1 Exit Criteria:**
- [ ] ...

---

### Phase 2: [Core Logic]

> **Goal:** _What this phase achieves_
> **Estimated Effort:** X days
> **Depends on:** Phase 1

- [ ] Step 2.1 — description
- [ ] Step 2.2 — description
- [ ] Step 2.3 — description

**Phase 2 Exit Criteria:**
- [ ] ...

---

### Phase 3: [Integration / Polish]

> **Goal:** _What this phase achieves_
> **Estimated Effort:** X days
> **Depends on:** Phase 2

- [ ] Step 3.1 — description
- [ ] Step 3.2 — description
- [ ] Step 3.3 — description

**Phase 3 Exit Criteria:**
- [ ] ...

---

## 3. Boundaries — Do NOT Touch

> These files, modules, and APIs are explicitly out of scope. Any changes to them require a separate task and review.

| Area | Path / Identifier | Reason |
|------|-------------------|--------|
| ...  | `src/...`         | Stable public API; changes break downstream consumers |
| ...  | `lib/...`         | Owned by another team; coordinate separately |
| ...  | `db/migrations/...` | Schema changes require a dedicated migration plan |

**Rule of thumb:** If your change requires modifying anything listed above, stop and revisit the plan.

---

## 4. Test Coverage

### Testing Strategy

| Level | Scope | Tool / Framework |
|-------|-------|------------------|
| Unit  | Individual functions and classes | ... |
| Integration | Module interactions, API contracts | ... |
| E2E | Critical user flows | ... |

### Required Test Cases

#### Unit Tests

- [ ] `describe('...')` — what it validates
- [ ] `describe('...')` — what it validates

#### Integration Tests

- [ ] Scenario: ...
- [ ] Scenario: ...

#### Edge Cases & Error Handling

- [ ] What happens when input is empty / malformed
- [ ] What happens when dependency is unavailable
- [ ] What happens under concurrent access

### Coverage Target

- Minimum line coverage: **X%**
- All public APIs must have tests
- All error paths must have tests

---

## 5. Key Decisions

> Record architectural and design decisions made during planning. Use this as a lightweight ADR (Architecture Decision Record).

### Decision 1: [Short Title]

- **Context:** _What problem or choice we faced_
- **Options Considered:**
  1. Option A — pros / cons
  2. Option B — pros / cons
- **Decision:** Option X
- **Rationale:** _Why this was chosen_
- **Consequences:** _What follows from this choice_

### Decision 2: [Short Title]

- **Context:** ...
- **Options Considered:** ...
- **Decision:** ...
- **Rationale:** ...
- **Consequences:** ...

---

## 6. Precautions

> Things that can go wrong and how to guard against them.

### Technical Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| ... | High/Med/Low | High/Med/Low | ... |
| ... | High/Med/Low | High/Med/Low | ... |

### Rollback Plan

_If the deployment fails or causes regressions:_

1. ...
2. ...
3. ...

### Migration Notes

_If this change involves data migration or breaking changes:_

- [ ] Backward compatibility: ...
- [ ] Feature flag: ...
- [ ] Migration script: ...

### Performance Considerations

- Expected impact on latency: ...
- Expected impact on memory / CPU: ...
- Load testing plan: ...

### Security Considerations

- [ ] Input validation: ...
- [ ] Auth / permissions: ...
- [ ] Sensitive data handling: ...

---

## Changelog

| Date | Author | Change |
|------|--------|--------|
| YYYY-MM-DD | name | Initial draft |
