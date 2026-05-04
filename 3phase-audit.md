---
name: 3phase-audit
description: >
  Three-Phase Structured Audit — Adversarial critique, constructive repair, knowledge distillation.
  Use for code reviews, document audits, system design reviews, and critical decisions.
version: 1.0.0
author: Bill
license: MIT
category: quality-assurance
tags: [audit, code-review, security, analysis, debugging, three-phase, adversarial]
trigger_keywords:
  - audit
  - review
  - critic
  - 3phase
  - three-phase audit
  - code review
  - security review
  - find bugs
  - adversarial review
---

# 3PHASE Audit — Three-Phase Structured Review

A structured, adversarial audit protocol that forces completeness through three mandatory phases. Each phase has a distinct role: destroy, rebuild, and distill.

## Why This Skill?

Most code reviews and audits are superficial — they identify obvious issues but miss structural weaknesses, hidden assumptions, and edge cases. The three-phase protocol solves this by:

1. **Forcing adversarial thinking** — Phase 1 must attack, not understand
2. **Mandating reconstruction** — Phase 2 must produce working fixes, not just suggestions
3. **Distilling reusable knowledge** — Phase 3 turns one audit into lasting patterns

## Core Principles

| Principle | Meaning | Prohibited |
|-----------|---------|------------|
| **P1 Modular Composition** | Modular, composable, standardized interfaces | Hardcoded dependencies |
| **P2 Sovereign Independence** | Each phase has clear responsibility; agents cannot make decisions for users | Unauthorized decisions |
| **P3 Script Centralization** | Core logic is scriptable and reusable | Logic scattered across contexts |
| **P4 Memory Sovereignty** | Insights must be persisted; experience must not vanish with the session | Knowledge lost after session ends |

## Operational Principles

| Principle | Requirement | Verification |
|-----------|------------|--------------|
| **Traceable** | Every step recorded, decision chain complete | Audit trail exists |
| **Explainable** | Every conclusion has reasoning; assumptions annotated | Output is self-documenting |
| **Reversible** | Changes can be rolled back; no destructive one-way operations | Rollback is possible |

---

## Invocation

```
AUDIT/3PHASE/
Target: <code | document | system-design | decision>
Constraint (optional): <performance | security | maintainability>
Depth (optional): <brief | standard | deep>
```

### Trigger Conditions

Auto-trigger when:
- User says: `audit`, `review`, `critic`, `find bugs`, `3phase`
- New system design is proposed
- Critical decision (irreversible / high-cost)
- Pre-deployment / pre-release
- After an incident or failure

---

## Execution Protocol

### Phase 1: ⚔️ Adversary (Critic Mode)

**Core objective**: Not to understand — but to destroy structural stability.

You are an attacker. Your job is to find every way this thing can break.

#### Mandatory Scan Dimensions

**1. Logic Flaws**
- Unclosed conditions (if without else, try without catch)
- Hidden premises (unstated assumptions treated as facts)
- Reasoning gaps (steps missing between conclusion and evidence)

**2. Edge Cases**
- Empty input / extreme values / illegal input
- Concurrency / race conditions / timing issues
- State machine incompleteness (missing transitions)

**3. Complexity & Resource Risks**
- Time complexity (flag O(n²), O(2ⁿ) explicitly)
- Unbounded memory growth
- I/O or network bottlenecks (blocking calls, no timeouts)

**4. Security & Robustness**
- Input injection (SQL / XSS / command injection)
- Permission boundaries (privilege escalation)
- Untrusted dependencies (supply chain risks)

#### Output Format

```
[CRITIC]

1. Fatal Issues
   - ...

2. High-Risk Issues
   - ...

3. Structural Weaknesses
   - ...

4. Strongest Counterexample
   - ...

5. Patch Directions
   - ...
```

**Iron rule**: No "mild" assessments. Finding zero issues is the biggest issue.

---

### Phase 2: 🤝 Builder (Repair Mode)

**Core objective**: Not to suggest — but to make it run reliably.

#### Mandatory Actions

**1. Structural Refactor (must output)**
- Rewrite core logic (actual code, not explanations)
- Eliminate hidden assumptions (make them explicit)
- Define clear input/output boundaries

**2. Test Generation (must simulate)**
Generate at minimum:
- Unit tests
- Boundary tests (edge cases)
- Stress tests
- Counterexample tests (from Phase 1)

**3. Uncertainty Annotation (mandatory)**
Explicitly state:
```
[UNCERTAINTY]
- What still depends on assumptions
- What needs real-world validation
- What requires user decision
```

#### Output Format

```
[BUILDER]

1. Refactor Plan
   - ...

2. Fixed Structure (or code)
   - ...

3. Test Cases (minimum 5 categories)
   - Unit tests: ...
   - Boundary tests: ...
   - Stress tests: ...
   - Counterexample tests: ...

4. Remaining Uncertainties
   - ...
```

---

### Phase 3: 🎓 Teacher (Distillation Mode)

**Core objective**: Turn one audit into a reusable cognitive module.

#### Three-Layer Distillation

**1. Reusable Principles**
Extract core lessons from this audit:
- "All hidden premises must be made explicit"
- "Complexity must be constrained at design time"
- ...

**2. Failure Pattern Library**
Record the typical errors found:
- Implicit state dependency
- Unhandled empty input
- Complexity runaway
- ...

**→ Persist to memory**: Use your agent's memory system to store these patterns for future audits.

**3. Transferable Templates**
Output reusable structures:
- Input validation template
- State machine template
- Error handling framework
- ...

#### Output Format

```
[TEACHER]

1. Core Principles
   - ...

2. Failure Patterns
   - ...

3. Reusable Templates
   - ...
```

---

## Verification Criteria

| Phase | Pass Condition |
|-------|---------------|
| Phase 1 | At least 1 fatal or high-risk issue found |
| Phase 2 | Test cases cover all Phase 1 counterexamples |
| Phase 3 | Experience persisted to memory system |

## Known Pitfalls

| Pitfall | Defense |
|---------|---------|
| Skipping Phase 1 to fix directly | Violation — not allowed |
| Uncertainties not annotated | Must explicitly mark [UNCERTAINTY] |
| Failure patterns not persisted | Knowledge lost — repeated mistakes |
| Mild evaluation | Must have adversarial density |
| Assumptions not verified | Must list in output |

## Adaptation Notes

This skill is framework-agnostic. To adapt for your agent:

- **Memory persistence**: Replace `sonuv_remember` with your agent's memory tool (e.g., `memory.save()`, file write, vector DB insert)
- **Trigger keywords**: Add to your agent's skill matching system
- **Output format**: The `[CRITIC]` / `[BUILDER]` / `[TEACHER]` markers are designed to be parseable by downstream tooling
- **Test generation**: Phase 2's "simulate" means mentally walk through test scenarios — actual test execution is optional but recommended

## Example Usage

### For Code Review

```
AUDIT/3PHASE/
Target: src/auth/login.py
Constraint: security
Depth: deep
```

### For System Design

```
AUDIT/3PHASE/
Target: Microservice migration plan
Constraint: maintainability
Depth: standard
```

### For Decision

```
AUDIT/3PHASE/
Target: "Should we use GraphQL or REST for the new API?"
Depth: standard
```

---

## License

MIT
